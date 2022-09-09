<template>
  <h1>Ninja Reaction Timer</h1>
  <button @click="start" :disabled="isPlaying">play</button>
  <!-- :disabled is an html attribute which get's added when isPlaying is true -->
  <Block  v-if="isPlaying" v-bind:delay="delay" @end="endGame" />
  <!-- <p v-if="showResults">Reaction time: {{score}} ms</p> -->
  <Results :score="score" v-if="showResults"></Results>
</template>

<script>
import Block from './components/Block.vue'
import Results from './components/Results.vue'

export default {
  name: 'App',
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResults: false
    }
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000 
      //Math.random() gets us a random number between 0 and 1, the max wait time will be 7sec and least will be 2secs
      this.isPlaying = true,
      this.showResults = false
    },
    endGame(reactionTime) {
      this.score = reactionTime,
      this.isPlaying = false,
      this.showResults = true
    }
  },
  components: {
    Block,
    Results
}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}

button {
  background: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 1rem;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}

button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
