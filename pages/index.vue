<template>
  <div class="h-screen flex justify-center items-center m-auto background">
    <div class="max-w-7xl p-1 rounded-md "> 
      <div class="text-white">
        <Header/>

        <div class="pt-10 body px-40 flex flex-row justify-evenly">
          <!-- First Row of Inputs -->
          <div class="flex flex-col justify-evenly">
            <div
              class="flex p-2"
              v-for="(input, i) in inputs"
              :key="i"
            >
              <span class="p-1 font-semibold">
                {{input}}L
              </span>

              <input
                class="js-input-base w-24 bg-gray-200 focus:bg-gray-300 rounded-lg"
                type="text"
                maxlength="4"
                placeholder="0000"
              >
            </div>
          </div>

          <!-- Second Row of Inputs -->
          <div class="flex flex-col justify-evenly">
            <div
              class="flex p-2"
              v-for="(input, i) in inputs"
              :key="i"
            >
              <span class="p-1 font-semibold">
                {{input}}H
              </span>

              <input
                class="js-input-base w-24 bg-gray-200 focus:bg-gray-300 rounded-lg"
                type="text"
                maxlength="4"
                placeholder="0000"
              >
            </div>
          </div>

          <div class="flex-col justify-evenly">
            <h3>
              Pierwszy i drugi adres instrukcji
            </h3>

            <div class="flex-row flex justify-center">
              <FirstSetOfInstructions />

              <SecondSetOfInstructions />
            </div>
          </div>

          <!-- Buttons -->
          <div class="p-2 flex flex-col justify-evenly">
            <button
              class="bg-gray-500 px-4 py-2 font-semibold text-sm text-white rounded-lg shadow-sm hover:bg-gray-600"
              @click="saveInputValues()"
            >
              Zapisz
            </button>

            <button
              class="bg-gray-500 px-4 py-2 font-semibold text-sm text-white rounded-lg shadow-sm hover:bg-gray-600"
              @click="randomHexForInputs()"
            >
              Randomowe Dane
            </button>

            <button
              class="px-4 py-2 font-semibold text-sm bg-gray-500 text-white rounded-lg shadow-sm hover:bg-gray-600"
              @click="resetValuesForInputs()"
            >
              Reset
            </button>
          </div>
        </div>

        <div class="body px-40 pt-10 flex flex-row justify-evenly">
          <!-- Misc Buttons -->
          <div class="p-2 flex flex-col justify-around items-center">
            <h4>
              Data Movement Instructions:
            </h4>

            <div class="px-1">
              <input type="radio" name="dataMovementInstructions" value="MOV" class="px-1">

              <label>MOV</label>
            </div>

            <div class="px-1">
              <input type="radio" name="dataMovementInstructions" value="XCHG" class="px-1">

              <label>XCHG</label>
            </div>
          </div>

          <div class="w-1/2 flex items-center justify-center">
            <button
              class="px-4 py-2 w-full font-semibold text-sm bg-green-800 text-white rounded-lg shadow-sm hover:bg-green-900"
              @click="startTheSimulation()"
            >
              Symuluj
            </button>
          </div>
        </div>

        <div class="body px-40 py-10 flex flex-row justify-evenly">
          <div>
            <span class="bold">AL:</span>
            <span class="js-result js-1 border border-gray-400 p-1 rounded-lg">
              0000
            </span>
          </div>

          <div>
            <span class="bold">BL:</span>
            <span class="js-result js-1 border border-gray-400 p-1 rounded-lg">
              0000
            </span>
          </div>

          <div>
            <span class="bold">CL:</span>
            <span class="js-result js-1 border border-gray-400 p-1 rounded-lg">
              0000
            </span>
          </div>

          <div>
            <span class="bold">DL:</span>
            <span class="js-result js-1 border border-gray-400 p-1 rounded-lg">
              0000
            </span>
          </div>

          <div></div>

          <div>
            <span class="bold">AH:</span>
            <span class="js-result js-1 border border-gray-400 p-1 rounded-lg">
              0000
            </span>
          </div>

          <div>
            <span class="bold">BH:</span>
            <span class="js-result js-1 border border-gray-400 p-1 rounded-lg">
              0000
            </span>
          </div>

          <div>
            <span class="bold">CH:</span>
            <span class="js-result js-1 border border-gray-400 p-1 rounded-lg">
              0000
            </span>
          </div>

          <div>
            <span class="bold">DH:</span>
            <span class="js-result js-1 border border-gray-400 p-1 rounded-lg">
              0000
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import Header from '~/components/Header.vue';
import FirstSetOfInstructions from '~/components/FirstSetOfInstructions.vue'
import SecondSetOfInstructions from '~/components/SecondSetOfInstructions.vue'

export default Vue.extend({
  name: 'IndexPage',
  components: {
    Header,
    FirstSetOfInstructions,
    SecondSetOfInstructions,
  },
  data: () => ({
    inputs: ['A', 'B', 'C', 'D'],
    inputValues: [],
    inputIndexes: {AL:0, BL:1, CL:2, DL:3, AH:4, BH:5, CH:6, DH:7},
    genRanHex: size => [...Array(size)].map(() => Math.floor(Math.random() * 16).toString(16)).join(''),
    displayEffect: finallTable => {
      const outputs = [...document.querySelectorAll('.js-result')];

      let i = 0;
      outputs.forEach(output => {
        output.innerText = finallTable[i];

        i++;
      });
    },
  }),
  methods: {
    resetValuesForInputs() {
      const inputsElements = [...document.querySelectorAll('.js-input-base')];

      inputsElements.forEach(input => {
        input.value = null;
      });
    },
    randomHexForInputs() {
      const inputsElements = [...document.querySelectorAll('.js-input-base')];

      inputsElements.forEach(input => {
        input.value = this.$data.genRanHex(4);
      });
    },
    saveInputValues() {
      this.$data.inputValues = [];
      const inputsElements = [...document.querySelectorAll('.js-input-base')];

      inputsElements.forEach(input => {
        this.$data.inputValues.push(input.value);
      });

      this.$data.displayEffect(this.$data.inputValues);
    },
    startTheSimulation() {
      const simulationMethods = document.querySelector('input[name="dataMovementInstructions"]:checked');
      const firstAdress = document.querySelector('input[name="firstSetOfInstructions"]:checked');
      const secondAdress = document.querySelector('input[name="secondSetOfInstructions"]:checked');

      // Validacja danych
      if (!this.$data.inputValues.length) {
        alert('Brak zapisanych danych');

        return;
      }

      if (!simulationMethods || !firstAdress || !secondAdress) {
        alert('Nie wszystkie pola są zaznaczone');

        return;
      }

      if ('MOV' === simulationMethods.value) {
        const firstValueIndex = this.$data.inputIndexes[firstAdress.value];
        const secondValueIndex = this.$data.inputIndexes[secondAdress.value];
        const secondValue = this.$data.inputValues[secondValueIndex];

        this.$data.inputValues[firstValueIndex] = secondValue;

        this.$data.displayEffect(this.$data.inputValues)

        return;
      }

      if ('XCHG' == simulationMethods.value) {
        const firstValueIndex = this.$data.inputIndexes[firstAdress.value];
        const secondValueIndex = this.$data.inputIndexes[secondAdress.value];
        const firstValue = this.$data.inputValues[firstValueIndex];
        const secondValue = this.$data.inputValues[secondValueIndex];

        this.$data.inputValues[firstValueIndex] = secondValue;
        this.$data.inputValues[secondValueIndex] = firstValue;

        this.$data.displayEffect(this.$data.inputValues)

        return;
      }
    }
  }
})
</script>
