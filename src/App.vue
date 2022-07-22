<template>
  <h1>Birdle</h1>
  <WordGrid :solution="solution" :guesses="guesses"/>
  <KeyboardGrid @guess="submitGuess" @update="onTyping"/>
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
      guesses: ["", "", "", "", "", ""],
      guessCount: 0,
      currentGuess: "",
      solution: "avion",
    }
  },
  methods: {
    submitGuess: function(guess) {
      this.guesses[this.guessCount] = (guess);
      this.guessCount++;
    },
    onTyping: function(guess) {
      this.guesses[this.guessCount] = guess;
    },
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
