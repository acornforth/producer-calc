<template>
  <div @click="copyToClipboard"
       v-on:mouseover="hover=true"
       v-on:mouseleave="hover=false"
       class="relative border-1 rounded-lg border-gray-900 px-2 mx-1 shadow-inner bg-gray-800 text-right">
    <span class="text-3xl ml-2 mr-16">{{value}}</span>
    <div class="text-2xl text-center w-12 text-gray-900 mx-2 absolute right-0 bottom-0">{{unit}}</div>
    <i v-if="hover" class="absolute top-0 right-0 bg-green-900 text-xs p-1 rounded">click to copy</i>
  </div>
</template>

<script>

export default {
  name: "Value",
  data() {
    return {
      hover: false
    }
  },
  props: {
    value: Number,
    unit: String,
  },
  methods: {
    copyToClipboard () {
      navigator.clipboard.writeText(this.value)
    }
  }
}
</script>

<style scoped>

</style>
