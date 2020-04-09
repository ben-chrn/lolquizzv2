<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>

import Vue from 'vue'
import Vuex from 'vuex'
import VueRouter from 'vue-router'

import axios from 'axios'

import Home from './components/Home.vue'
import Game from './components/Game.vue'
import Results from './components/Results.vue'
import Rules from './components/Rules.vue'

Vue.use(Vuex)
Vue.use(VueRouter)

const store = new Vuex.Store({
  state: {
    champsCount: 0,
    champions: [],
    gameStarted: false,
    timer: 900
  },
  mutations: {
    storeChamps(state, champions) {
      state.champions = champions
    },
    storeChampsCount(state, count) {
      state.champsCount = count
    },
    decrementTimer(state) {
      state.timer--
    },
    resetTimer(state) {
      state.timer = 900
    },
  },
  actions: {
    decrementTimer() {
      store.commit('decrementTimer');
    },
    resetTimer() {
      store.commit('resetTimer');
    }
  },
  getters: {
    currentTime: state => {
      let minutes = Math.floor(state.timer/60)
      let seconds = Math.floor(state.timer - minutes*60)

      if(minutes < 10) {
        minutes = '0'+minutes
      }
      if(seconds < 10) {
        seconds = '0'+seconds
      }
      return `${minutes}:${seconds}`
    }
  }
})

const routes = [
  { path: '/', component: Home},
  { path: '/rules', component: Rules},
  { path: '/game', component: Game},
  { path: '/results', component: Results}
]

const router = new VueRouter({
  routes
})

export default {
  name: 'App',
  store,
  router,
  mounted() {
    this.buildChamps()
  },

  methods: {
    async buildChamps() {

      let champsFinal = []
      const allChamps = await axios.get('http://ddragon.leagueoflegends.com/cdn/10.7.1/data/en_US/champion.json')

      this.$store.commit('storeChampsCount', Object.keys(allChamps.data.data).length)
    
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

h1 {
  margin: 0;
  font-family: 'Optimus Princeps';
  font-size: 48px;
  line-height: 62px;
  color: #F4DE93;
  color: radial-gradient(33.21% 48.02% at 49.87% 54.67%, #F4DE93 0%, #AE914B 100%);
}

h2 {
  font-family: 'Proxima Nova';
  font-style: normal;
  font-weight: 600;
  font-size: 20px;
  line-height: 24px;
  color: #BDBDBD;
}

p, li {
  font-family: 'Proxima Nova';
  font-style: normal;
  font-weight: 600;
  font-size: 16px;
  line-height: 20px;

  color: #BDBDBD;
}

input {
  padding: 16px 24px;
  background: rgba(255, 255, 255, 0.1);
  /* Grey Content */
  border: 2px solid #BDBDBD;
  box-sizing: border-box;
  border-radius: 8px;
  outline: 0;
  color: #F4DE93;
  font-family: Proxima Nova;
  font-style: normal;
  font-weight: 600;
  font-size: 20px;
  line-height: 24px;
  text-align:center;
}

.button {
  display: flex;
  flex-direction: row;
  padding: 16px 24px;
  background: radial-gradient(33.21% 48.02% at 49.87% 54.67%, #F4DE93 0%, #AE914B 100%);
  border: none;
  border-radius: 8px;
  color: #11101E;
  text-decoration: none;

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
