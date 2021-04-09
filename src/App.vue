<template class="border rounded">
  <h1 class="text-4xl text-gray-300">Music Producer Calculator</h1>
  <h2 class="text-2xl text-gray-400">Pitch - Frequency - Period - Wavelength</h2>
  <Calculator/>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Calculator from './components/Calculator.vue'

export default defineComponent({
  name: 'App',
  components: {
    Calculator
  }
})
</script>
