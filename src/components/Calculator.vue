<template>
  <div class="mt-4 p-4 rounded-lg text-gray-200 bg-indigo-900">
    <label class="text-xl">Concert Pitch
      <button class="text-xl" @click="pitch -= 1">--</button>
      <button class="text-xl" @click="pitch -= 0.1">-</button>
      <input class="text-xl bg-indigo-800" type="text" :value="pitch">
      <button class="text-xl" @click="pitch += 0.1">+</button>
      <button class="text-xl" @click="pitch += 1">++</button>
    </label>
    <br>
    <label class="text-xl" for="note">
      Note
      <select  class="bg-indigo-800 text-xl"  name="note" id="note" v-model="note">
        <option v-for="(note, number) in notes" class="bg-indigo-800" :value="number">{{note}}</option>
      </select>
    </label>
    <label class="text-xl">Octave
      <button class="text-xl" @click="octave -= 1">--</button>
      <input class="text-xl bg-indigo-800 " type="text" :value="octave">
      <button class="text-xl" @click="octave += 1">++</button>
    </label>
    <div class="mt-3 text-green-400 text-4xl text-bold">
      <span>{{frequency}}Hz</span> |   <span>{{time}}ms</span> | {{length}}m
    </div>
  </div>
</template>


<script lang='ts'>
export default {
  name: 'Calculator',
  props: {
  },
  data() {
    return {
      count: 0,
      pitch: 440.0,
      octave: 0,
      note: 7,
      notes: {1: 'A', 2:'A#', 3: 'B', 4: 'C', 5: 'C#', 6: 'D', 7: 'D#', 8:'E', 9: 'F', 10: 'F#', 11: 'G', 12: 'G#'}
    }
  },
  computed: {
    frequency() {
      return this.round(
          this.pitch * Math.pow(Math.pow(2, (1/12)),(this.note-49+(12*this.octave))),
          4
      )
    },
    time() { // in ms
      return this.round(1000/this.frequency, 4)
    },
    length() { // speed of sound in air = 344 m/s
      return this.round(344 / this.frequency, 4)
    }
  },
  methods: {
    round: (n, precision) =>
        Math.round((Number.EPSILON + n) * Math.pow(10, precision)) / Math.pow(10, precision)
  }

}
</script>
