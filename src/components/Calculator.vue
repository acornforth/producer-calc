<template>
  <label class="text-xl">Concert Pitch
    <button class="text-xl" @click="pitch -= 1">--</button>
    <button class="text-xl" @click="pitch -= 0.1">-</button>
    <input class="text-xl" type="text" :value="pitch">
    <button class="text-xl" @click="pitch += 0.1">+</button>
    <button class="text-xl" @click="pitch += 1">++</button>
  </label>
  <br>
  <label for="note">
    Note
    <select name="note" id="note" v-model="note">
      <option value="1">A</option>
      <option value="2">A#</option>
      <option value="3">B</option>
      <option value="4">C</option>
      <option value="5">C#</option>
      <option value="6">D</option>
      <option value="7">D#</option>
      <option value="8">E</option>
      <option value="9">F</option>
      <option value="10">F#</option>
      <option value="11">G</option>
      <option value="12">G#</option>
    </select>
  </label>
  <label>Octave
    <button @click="octave -= 1">--</button>
    <input type="text" :value="octave">
    <button @click="octave += 1">++</button>
  </label>
  <br>
  <span>{{frequency}}Hz</span> |   <span>{{time}}ms</span> | {{length}}m
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
      note: 7
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
