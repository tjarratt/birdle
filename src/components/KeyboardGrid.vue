<template>
  <div id=wrapper>
    <div class=grid>
      <div class=row>
        <button @click=onTap class=row-key :class="classObject('q')">Q</button>
        <button @click=onTap class=row-key :class="classObject('w')">W</button>
        <button @click=onTap class=row-key :class="classObject('e')">E</button>
        <button @click=onTap class=row-key :class="classObject('r')">R</button>
        <button @click=onTap class=row-key :class="classObject('t')">T</button>
        <button @click=onTap class=row-key :class="classObject('y')">Y</button>
        <button @click=onTap class=row-key :class="classObject('u')">U</button>
        <button @click=onTap class=row-key :class="classObject('i')">I</button>
        <button @click=onTap class=row-key :class="classObject('o')">O</button>
        <button @click=onTap class=row-key :class="classObject('p')">P</button>
      </div>
      <div class=row>
        <button @click=onTap class=row-key :class="classObject('a')">A</button>
        <button @click=onTap class=row-key :class="classObject('s')">S</button>
        <button @click=onTap class=row-key :class="classObject('d')">D</button>
        <button @click=onTap class=row-key :class="classObject('f')">F</button>
        <button @click=onTap class=row-key :class="classObject('g')">G</button>
        <button @click=onTap class=row-key :class="classObject('h')">H</button>
        <button @click=onTap class=row-key :class="classObject('j')">J</button>
        <button @click=onTap class=row-key :class="classObject('k')">K</button>
        <button @click=onTap class=row-key :class="classObject('l')">L</button>
      </div>
      <div class=row>
        <button @click=onReturn id=key-return class=row-key>ENTER</button>
        <button @click=onTap class=row-key :class="classObject('z')">Z</button>
        <button @click=onTap class=row-key :class="classObject('x')">X</button>
        <button @click=onTap class=row-key :class="classObject('c')">C</button>
        <button @click=onTap class=row-key :class="classObject('v')">V</button>
        <button @click=onTap class=row-key :class="classObject('b')">B</button>
        <button @click=onTap class=row-key :class="classObject('n')">N</button>
        <button @click=onTap class=row-key :class="classObject('m')">M</button>
        <button @click=onBackspace class=row-key>⬅</button>
      </div>
    </div>
  </div>

  <input id=hiddenfield autofocus maxlength=5 @keyup="onKeyup" unselectable="on" onselectstart="return false" />
</template>

<script>
import dictionary from '../dictionary.js'

export default {
  name: 'KeyboardGrid',
  props: { hints: Object },
  emits: ["guess", "update", "invalid"],
  data() {
    return {
      currentGuess: "",
    }
  },
  methods: {
    onTap: function(event) {
      let character = event.srcElement.innerText;
      this._didType(character);
    },
    onBackspace: function() {
      this._didTypeBackspace();
    },
    onReturn: function() {
      this._didTypeReturn();
    },
    onKeyup: function(event) {
      if (event.keyCode == 13) {
        this._didTypeReturn();
        return;
      }
      if (event.keyCode == 8) {
        this._didTypeBackspace();
        return;
      }
      if (event.keyCode < 65 || event.keyCode > 90) {
        return;
      }
      if (this.currentGuess.length >= 5) {
        return;
      }

      this._didType(event.key);
    },
    classObject(char) {
      return {
        correct: this.hints[char] == "correct",
        misplaced: this.hints[char] == "misplaced",
        wrong: this.hints[char] == "wrong",
      };
    },
    _didTypeBackspace() {
      this.currentGuess = this.currentGuess.slice(0, -1);
      this.$emit("update", this.currentGuess);
    },
    _didTypeReturn() {
      if (this._isNotInDictionary(this.currentGuess)) { this.$emit("invalid"); return; }
      if (this.currentGuess.length != 5) { return; }

      this.$emit("guess", this.currentGuess);
      this.currentGuess = "";
      document.getElementById("hiddenfield").value = "";
    },
    _didType(letter) {
      this.currentGuess += letter.toLowerCase();
      this.$emit("update", this.currentGuess);
    },
    _isNotInDictionary(word) {
      return dictionary.indexOf(word) == -1;
    },
  },
}

</script> 

<style scoped>

#wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}

.grid {
  display: grid;
  grid-template-rows: repeat(3, 1fr);
  grid-gap: 5px;
  padding: 10px;
}

.row {
  display: grid;
  grid-gap: 5px;
  grid-template-columns: repeat(10, 1fr);
}

.row-key {
  display: grid;
  grid-gap: 5px;

  font-weight: bold;
  height: 58px;
  min-width: 1em;
  color: white;
  background-color: #818384;
  border-radius: 4px;
  border: 0;
  padding: 0 3px;
  margin: 0 6px 0 0;

  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;

  cursor: pointer;
}

.row-key.correct {
  background-color: #538D4E;
}

.row-key.misplaced {
  background-color: #B29F4C;
}

.row-key.wrong {
  background-color: #3A3A3C;
}


</style>
