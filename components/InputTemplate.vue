<template>
  <div class="px-1">
    <input
      type="radio"
      name="{{radioMainName}}"
      :value="name"
    >

    <label>
      {{ name }}
    </label>
  </div>
</template>

<script>
export default {
  name: 'InputTemplate',
  props: {
    name: String,
    radioMainName: String,
  },
}
</script>