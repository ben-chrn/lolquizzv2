<template>
  <div id="game">
    <div class="game__content">
      <button 
        class="button"
        v-on:click="startGame"
      >Start</button>
      <button 
        class="button"
        v-on:click="resetTimer"
      >Reset</button>
      <button 
        class="button"
        v-on:click="pauseTimer"
      >Pause</button>
      <p>{{ currentTime }}</p>
      <Champions />
      <Sidebar />
    </div>
  </div>
</template>

<script>

import Champions from './Champions.vue'
import Sidebar from './Sidebar.vue'

export default {
  name: 'Game',
  components: {
    Champions,
    Sidebar,
  },
  computed: {
    currentTime() {
      return this.$store.getters.currentTime
    }
  },
  methods: {
    startGame() {
      this.interval = setInterval(() => { this.$store.dispatch('decrementTimer')}, 1000)
    },
    pauseTimer() {
      clearInterval(this.interval)
    },
    resetTimer() {
      clearInterval(this.interval)
      this.$store.dispatch('resetTimer')
    }
  }
}

</script>

<style>
</style>