<template>
  <h1>Birdle</h1>
  <WordGrid :solution="solution" :guesses="guesses"/>
  <KeyboardGrid @guess="submitGuess" @update="onTyping"/>
</template>

<script>
import WordGrid from './components/WordGrid.vue'
import KeyboardGrid from './components/KeyboardGrid.vue'

function emptyState() {
  return [
    { value: "", state: "wrong"},
    { value: "", state: "wrong"},
    { value: "", state: "wrong"},
    { value: "", state: "wrong"},
    { value: "", state: "wrong"},
  ];
}


export default {
  name: 'App',
  components: {
    WordGrid,
    KeyboardGrid,
  },
  data() {
    return {
      guesses: [emptyState(), emptyState(), emptyState(), emptyState(), emptyState(), emptyState() ],
      guessCount: 0,
      solution: "avion",
    }
  },
  methods: {
    submitGuess: function(rawInput) {
      this.guesses[this.guessCount] = this._guess(rawInput);
      this.guessCount++;
    },
    onTyping: function(rawInput) {
      this.guesses[this.guessCount] = this._guess(rawInput);
    },
    _guess: function(rawInput) {
      return rawInput.padEnd(5).split("").map((c) => ({value: c, state: "wrong"}));
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
