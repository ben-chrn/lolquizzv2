<template>
  <div id="game">
    <Champions />
    <Sidebar />
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

<style lang="scss" scoped>

  div#game {
    display:flex;
    flex-direction: row;

    div#champions {
      width: 75%;
    }

    div#sidebar { 
      width: 25%;
    }
  }
</style>