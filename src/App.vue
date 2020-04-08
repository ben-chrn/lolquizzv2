<template>
  <div id="app">
    <Home />
    <Champions />
  </div>
</template>

<script>

import Vue from 'vue'
import Vuex from 'vuex'
import axios from 'axios'
import Home from './components/Home.vue'
import Champions from './components/Champions.vue'

Vue.use(Vuex)

const store = new Vuex.Store({
  state: {
    champions: [],
  },
  mutations: {
    storeChamps(state, champions) {
      state.champions = champions
    },
  },
  actions: {
    toggleChamp(state, champions, championIndex) {
      state.champions[championIndex].isRevealed = !state.champions[championIndex].isRevealed
    }
  }
})

export default {
  name: 'App',
  store,
  components: {
    Home,
    Champions,
  },

  mounted() {
    this.buildChamps()
  },

  methods: {
    async buildChamps() {

      let champsFinal = []
      const allChamps = await axios.get('http://ddragon.leagueoflegends.com/cdn/10.7.1/data/en_US/champion.json')
    
      for await (const champName of Object.keys(allChamps.data.data)) {
        let champObj = await this.getSingleChamp(champName)
        champsFinal.push(champObj)
      }

      this.$store.commit('storeChamps', champsFinal);
    },

    async getSingleChamp(champName) {

      let champion = await axios.get(`http://ddragon.leagueoflegends.com/cdn/10.7.1/data/en_US/champion/${champName}.json`)
      champion = Object.entries(champion.data.data)[0][1];

      const randNumber = Math.floor(Math.random() * champion.skins.length) + 1
      
      let champObj = {
        name: champion.name,
        title: champion.title,
        isRevealed: false,
        loadingUrl: `http://ddragon.leagueoflegends.com/cdn/img/champion/loading/${champion.name}_${randNumber}.jpg`,
        splashUrl: `http://ddragon.leagueoflegends.com/cdn/img/champion/splash/${champion.name}_${randNumber}.jpg`,
      }

      return champObj
    }
  }
}
</script>

<style>

@font-face {
  font-family: "Proxima Nova";
  src: url("assets/fonts/ProximaNova-Semibold.woff") format("woff");
  src: url("assets/fonts/ProximaNova-Semibold.woff2") format("woff2");
}

@font-face {
  font-family: "Optimus Princeps";
  src: url("assets/fonts/OptimusPrincepsSemiBold.woff") format("woff");
  src: url("assets/fonts/OptimusPrincepsSemiBold.woff2") format("woff2");
}

body {
  margin: 0;
}

#app {
  background: #11101E;
  height: 100vh;
  width: 100vw;
}

h2 {
  font-family: 'Proxima Nova';
  font-style: normal;
  font-weight: 600;
  font-size: 20px;
  line-height: 24px;
  color: #BDBDBD;
}

button {
  display: flex;
  flex-direction: row;
  padding: 16px 24px;
  background: radial-gradient(33.21% 48.02% at 49.87% 54.67%, #F4DE93 0%, #AE914B 100%);
  border: none;
  border-radius: 8px;
  color: #11101E;

  font-family: 'Proxima Nova';
  font-style: normal;
  font-weight: 600;
  font-size: 16px;
  line-height: 19px;
  text-transform: uppercase;
  outline: none;
  cursor: pointer;
}

</style>
