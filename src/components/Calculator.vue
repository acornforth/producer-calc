<template>
  <div class="mt-4 p-4 rounded-lg text-gray-200 bg-indigo-900">
    <label class="text-xl my-1 block">Concert Pitch</label>
    <button @click="pitch -= 1">--</button>
    <button @click="pitch -= 0.1">-</button>
    <input class="text-xl bg-indigo-800 rounded-lg w-24 shadow-inner py-2 text-center" type="text" v-model="pitch">
    <button @click="pitch += 0.1">+</button>
    <button @click="pitch += 1">++</button>
    <label class="text-xl block my-1" for="note">Note</label>
    <select  class="bg-indigo-800 text-xl rounded-lg w-24 shadow-inner p-2 text-center"  name="note" id="note" v-model="note">
      <option v-for="(note, number) in notes" class="bg-indigo-800" :value="number">{{note}}</option>
    </select>
    <label class="text-xl block my-1">Octave</label>
    <button @click="octave -= 1">--</button>
    <input class="text-xl bg-indigo-800 rounded-lg w-24 shadow-inner py-2 text-center" type="text" v-bind:value="octave">
    <button @click="octave += 1">++</button>
    <div class="mt-3 lg:flex justify-between">
      <Value class="flex-1" :value="frequency" unit="Hz"/>
      <Value class="flex-1" :value="time" unit="ms"/>
      <Value class="flex-1" :value="length" unit="m"/>
      <Value class="flex-1" :value="bpm1" unit="bpm"/>
    </div>
  </div>
</template>


<script lang='ts'>
import Value from './Value.vue'
export default {
  name: 'Calculator',
  components: {
    Value
  },
  props: {
  },
  data() {
    return {
      count: 0,
      refpitch: 440.0,
      octave: 0,
      note: 7,
      notes: {1: 'A', 2:'A♯/B♭', 3: 'B', 4: 'C', 5: 'C♯/D♭', 6: 'D', 7: 'D♯/E♭', 8:'E', 9: 'F', 10: 'F♯/G♭', 11: 'G', 12: 'G♯/A♭'}
    }
  },
  computed: {
    frequency() {
      return this.round(
          this.pitch * Math.pow(Math.pow(2, (1/12)),(this.note-49+(12*this.octave))),
          4
      )
    },
    pitch: {
      get() {
        return this.refpitch.toFixed(1)
      },
      set(value: string) {
        this.refpitch = parseFloat(value)
      }
    },
    time() { // in ms
      return this.round(1000/this.frequency, 4)
    },
    length() { // speed of sound in air = 344 m/s
      return this.round(344 / this.frequency, 4)
    },
    bpm1(dur) {
      return this.round(this.frequency * 3600/512, 3);
    },
  },
  methods: {
    round: (n, precision) =>
        Math.round((Number.EPSILON + n) * Math.pow(10, precision||0)) / Math.pow(10, precision||0)
  }

}
</script>
