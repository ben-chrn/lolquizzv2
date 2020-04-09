<template>
  <div id="rules">
    <h1>Rules</h1>
    <ol>
      <li>You have 15:00 to find the {{champsCount}} champions of League of Legends.</li>
      <li>Play fair (don't use a list of the champions on your second screen, obviously).</li>
      <li>Enter your guess in the <input value="Input" disabled /> and press enter.</li>
      <li>Have fun :)</li>
    </ol>
    <router-link
      to="/game"
      class="button"
    >I'm ready!</router-link>
  </div>
</template>

<script>

export default {
  name: 'Rules',
  computed: {
    champsCount() {
      return this.$store.state.champsCount
    },
  },
}

</script>

<style lang="scss">

  div#rules {
    display:flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: fixed;
    z-index: 2;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(#11101E, .8);

    ol {
      margin: 24px 36px;

      li {
        margin: 8px 0;

        input {
          width:150px;
          padding: 8px 8px;
          margin: 0 8px;
          
        }
      }
    }
  }

</style>