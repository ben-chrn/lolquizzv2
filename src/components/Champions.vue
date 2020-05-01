<template>
  <div id="champions">
    <template v-for="champion in champions">
      <Champion
        class="champName"
        :key="champion.name"
        :champion="champion"
      >{{ champion.name }}</Champion>
    </template>
  </div>
</template>

<script>

import Champion from './Champion.vue'

export default {
  name: 'Champions',
  components: {
    Champion,
  },
  computed: {
    champions() {
      return this.$store.state.champions
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

  div#champions {
    padding: 48px;
    height: 100vh;
    overflow-y: scroll;
  }
</style>
