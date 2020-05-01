<template>
  <div id="sidebar">
    <div class="sidebar__top"></div>
    <div class="sidebar__middle">
    </div>
    <div class="sidebar__bottom">
      <span class="champsCount">{{ foundCount }}</span>
      <input />
      <span class="currentTime">{{ currentTime }}</span>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Sidebar',
    computed: {
      currentTime() {
        return this.$store.getters.currentTime
      },
      
      foundCount() {
        return "0/192"
      }
    },
  }
</script>

<style scoped lang="scss">

  div#sidebar {
    display:flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    height: 100vh;
    padding: 55px;


    div.sidebar__bottom {

      display:flex; 
      flex-direction: column;
      justify-content: flex-start;
      align-items: center;

      span.champsCount {
        font-family: "OptimusPrinceps";
        font-size: 24px;
        color: #F4DE93;
      }

      input {
        margin: 24px 0;
      }

      span.currentTime {
        font-family: "OptimusPrinceps";
        font-size: 48px;
        color: #F4DE93;
      }
    }
  }

</style>