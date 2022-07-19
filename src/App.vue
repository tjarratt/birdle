<template>
  <h1>Birdle</h1>
  <WordGrid :guesses="guesses"/>
  <KeyboardGrid @guess="onGuess"/>
</template>

<script>
import WordGrid from './components/WordGrid.vue'
import KeyboardGrid from './components/KeyboardGrid.vue'

export default {
  name: 'App',
  components: {
    WordGrid,
    KeyboardGrid,
  },
  data() {
    return {
      guesses: [],
    }
  },
  methods: {
    onGuess: function(guess) {
      this.guesses.push(guess);
    }
  },
}
</script>

<style>
body {
  margin: 0;
  background-color: #121213;
}
#app {
  margin: 0;

  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
