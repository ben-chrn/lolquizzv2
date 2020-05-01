<template>
  <div class="championSingle">
    <div 
      class="championRevealed"
      v-if="champion.isRevealed"
    >
      <img v-bind:src="champion.squareUrl" />
    </div>
    <div 
      v-else
      class="championHidden"
    >
      <img src="../assets/images/unrevealed_bg.png">
      <span>?</span>
    </div>
  </div>
</template>

<script>
  export default {
    name:"Champion",
    props: {
      champion: Object,
    }
  }
</script>

<style scoped lang="scss">

  div.championSingle {
    width: 120px;
    height: 120px;
    overflow: hidden;
    border-radius: 8px;

    div.championRevealed, 
    div.championHidden {
      background: linear-gradient(300deg, rgba(255, 255, 255, 0) 33%, rgba(0, 0, 0, 0.28) 80%);
      position: relative;

      img {
        position: absolute;
        width: calc(100% + 3px);
        height: auto;
        top: -3px;
        left: -3px;
        opacity: .7;
      }

      span {
        position: absolute;
        font-family: "OptimusPrinceps";
        font-size: 74px;
        color: rgba(244, 222, 147, 0.2);
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%) rotate(13deg) ;
      }
    }
  }

</style>