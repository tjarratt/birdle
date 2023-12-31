<template>
  <h1>Birdle</h1>
  <PopToast v-if="toastMessage" @faded="onFaded" :message="toastMessage"/>
  <WordGrid :guesses="guesses"/>
  <KeyboardGrid :hints="keyHints" @guess="submitGuess" @update="onTyping" @invalid="onInvalidWord"/>
</template>

<script>
import WordGrid from './components/WordGrid.vue'
import KeyboardGrid from './components/KeyboardGrid.vue'
import PopToast from './components/PopToast.vue'
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
  return list[daysIntoYear(new Date()) % list.length];
}

function daysIntoYear(date){
    return (Date.UTC(date.getFullYear(), date.getMonth(), date.getDate()) - Date.UTC(date.getFullYear(), 0, 0)) / 24 / 60 / 60 / 1000;
}

function successToastMessage(attemptNumber) {
  return [
    "Genius", "Magnificient", "Impressive", "Splendid", "Great", "Phew",
  ][attemptNumber];
}

export default {
  name: 'App',
  components: {
    WordGrid,
    KeyboardGrid,
    PopToast,
  },
  data() {
    return {
      playable: true,
      guesses: [emptyState(), emptyState(), emptyState(), emptyState(), emptyState(), emptyState() ],
      guessCount: 0,
      solution: chooseRandomly(dictionary),
      keyHints: {},
      toastMessage: "",
    }
  },
  methods: {
    submitGuess: function(rawInput) {
      if (!this.playable) { return; }

      this.guesses[this.guessCount] = this._guess(rawInput, this._validate);

      if (rawInput == this.solution) {
        this.toastMessage = successToastMessage(this.guessCount);
        this.playable = false;
        return;
      }

      this.guessCount++;
      this.playable = this.guessCount < 6;
    },
    onTyping: function(rawInput) {
      if (!this.playable) { return; }

      this.guesses[this.guessCount] = this._guess(rawInput, this._alwaysWrong);
    },
    onInvalidWord: function() {
      if (!this.playable) { return; }

      this.toastMessage = "Ce n'est pas un mot valid";
      this.guesses[this.guessCount].invalid = true;
    },
    onFaded: function() {
      this.toastMessage = "";
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
        this.keyHints[char] = "correct";
        return "correct";
      } else if (this.solution.indexOf(char) > -1) {
        this.keyHints[char] ||= "misplaced";
        return "misplaced";
      } else {
        this.keyHints[char] = "wrong";
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

  touch-action: none;
  -webkit-touch-callout:none;
  -webkit-user-select:none;
  -khtml-user-select:none;
  -moz-user-select:none;
  -ms-user-select:none;
  user-select:none;
  -webkit-tap-highlight-color:rgba(0,0,0,0);
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
