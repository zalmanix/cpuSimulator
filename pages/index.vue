<template>
  <div>
    <Header/>

    <!-- <div class="bg-green-300"> -->
    <div>
      <div class="px-40 flex flex-row">
        <div class="flex flex-col">
          <div
            class="flex p-2"
            v-for="(input, i) in inputs"
            :key="i"
          >
            <span class="p-1 font-semibold">
              {{input}}H
            </span>

            <input
              class="js-input-base w-24 bg-blue-300 focus:bg-blue-400 rounded-lg"
              type="text"
              maxlength="4"
              placeholder="0000"
            >
          </div>
        </div>

        <div class="flex flex-col">
          <div
            class="flex p-2"
            v-for="(input, i) in inputs"
            :key="i"
          >
            <span class="p-1 font-semibold">
              {{input}}L
            </span>

            <input
              class="js-input-base w-24 bg-blue-300 focus:bg-blue-400 rounded-lg text-white"
              type="text"
              maxlength="4"
              placeholder="0000"
            >
          </div>
        </div>

        <div class="p-2 flex flex-col justify-around">
          <button class="px-4 py-2 font-semibold text-sm bg-green-500 text-white rounded-full shadow-sm hover:bg-green-600">
            Zapisz
          </button>

          <button class="px-4 py-2 font-semibold text-sm bg-purple-500 text-white rounded-full shadow-sm hover:bg-purple-600">
            Randomowe Dane
          </button>

          <button
            class="px-4 py-2 font-semibold text-sm bg-red-500 text-white rounded-full shadow-sm hover:bg-red-600"
            @click="resetValues"
          >
            Reset
          </button>
        </div>
      </div>


    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import Header from '~/components/Header.vue'

export default Vue.extend({
  name: 'IndexPage',
  components: {
    Header,
  },
  data: () => ({
   inputs: ['A', 'B', 'C', 'D'],
  }),
  setup() {
    function resetValues() {
      const inputs = document.querySelectorAll('.js-input-base');

      console.log(inputs)
    }

    return {
      resetValues
    }
  }
})

    Header</script>
