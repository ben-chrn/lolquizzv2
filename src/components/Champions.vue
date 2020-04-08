<template>
  <div class="champsList">
    <template v-for="champion in champions">
      <div 
        class="champName"
        :key="champion.name"
      >{{ champion.name }}</div>
    </template>
  </div>
</template>

<script>
export default {
  name: 'Champions',
  mounted() {
    console.log(this.$store)
  },
  computed: {
    champions() {
      return this.$store.state.champions
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
