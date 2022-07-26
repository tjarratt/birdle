<template>
  <h1>Birdle</h1>
  <WordGrid :solution="solution" :guesses="guesses"/>
  <KeyboardGrid @guess="submitGuess" @update="onTyping" @invalid="onInvalidWord"/>
</template>

<script>
import WordGrid from './components/WordGrid.vue'
import KeyboardGrid from './components/KeyboardGrid.vue'
import dictionary from './dictionary.js'

function emptyState() {
  return {
    invalid: false,
    input: [
      { value: "", state: "wrong"},
      { value: "", state: "wrong"},
      { value: "", state: "wrong"},
      { value: "", state: "wrong"},
      { value: "", state: "wrong"},
    ],
  }
}

function chooseRandomly(list) {
  let solution = list[daysIntoYear(new Date()) % list.length];
  return solution;
}

function daysIntoYear(date){
    return (Date.UTC(date.getFullYear(), date.getMonth(), date.getDate()) - Date.UTC(date.getFullYear(), 0, 0)) / 24 / 60 / 60 / 1000;
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
      solution: chooseRandomly(dictionary),
    }
  },
  methods: {
    submitGuess: function(rawInput) {
      this.guesses[this.guessCount] = this._guess(rawInput, this._validate);
      this.guessCount++;
    },
    onTyping: function(rawInput) {
      this.guesses[this.guessCount] = this._guess(rawInput, this._alwaysWrong);
    },
    onInvalidWord: function() {
      console.log("current word is invalid");
      this.guesses[this.guessCount].invalid = true;
    },
    _guess: function(rawInput, validator) {
      return {
        invalid: false,
        input: rawInput.padEnd(5).split("").map((c, i) => ({value: c, state: validator(c, i)})),
      };
    },
    _alwaysWrong: function() { return "wrong"; },
    _validate: function(char, index) {
      if (char === this.solution[index]) {
        return "correct";
      } else if (this.solution.indexOf(char) > -1) {
        return "misplaced";
      } else {
        return "wrong";
      }
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
