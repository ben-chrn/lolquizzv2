<template>
  <div id="home">
    <div class="home__content">
      <img src="../assets/images/logo.png" />
      <h2>Can you guess all X champions in League of legends in less than 15 minutes ?</h2>
      <button>Play now</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Home',
  // props: {
  // }
}

</script>

<style scoped lang="scss">

  div#home {
    background: url('../assets/images/home_bg.png');
    background-size: cover;
    background-position: center center;

    display:flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;

    height: 100vh;
    width: 100vw;

    div.home__content {
      display:flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;

      h2 {
        margin: 48px 0 24px;
      }
    }
  }

</style>