<template>
  <div>
    <Header/>

    <div class="bg-gray-50">
      <div 
        class="flex"
        v-for="(input, i) in inputs"
        :key="i"
      >
        <span>{{input}}H</span>

        <input class="block w-full text-sm text-slate-500" type="text">
      </div>

      <div 
        class="flex"
        v-for="(input, i) in inputs"
        :key="i"
      >
        <span>{{input}}L</span>

        <input type="text">
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
  })
})

    Header</script>
