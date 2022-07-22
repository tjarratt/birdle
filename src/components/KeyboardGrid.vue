<template>
  <div id=wrapper>
    <div class=grid>
      <div class=row>
        <button @click=onTap class=row-key>Q</button>
        <button @click=onTap class=row-key>W</button>
        <button @click=onTap class=row-key>E</button>
        <button @click=onTap class=row-key>R</button>
        <button @click=onTap class=row-key>T</button>
        <button @click=onTap class=row-key>Y</button>
        <button @click=onTap class=row-key>U</button>
        <button @click=onTap class=row-key>I</button>
        <button @click=onTap class=row-key>O</button>
        <button @click=onTap class=row-key>P</button>
      </div>
      <div class=row>
        <button @click=onTap class=row-key>A</button>
        <button @click=onTap class=row-key>S</button>
        <button @click=onTap class=row-key>D</button>
        <button @click=onTap class=row-key>F</button>
        <button @click=onTap class=row-key>G</button>
        <button @click=onTap class=row-key>H</button>
        <button @click=onTap class=row-key>J</button>
        <button @click=onTap class=row-key>K</button>
        <button @click=onTap class=row-key>L</button>
      </div>
      <div class=row>
        <button @click=onReturn id=key-return class=row-key>ENTER</button>
        <button @click=onTap class=row-key>Z</button>
        <button @click=onTap class=row-key>X</button>
        <button @click=onTap class=row-key>C</button>
        <button @click=onTap class=row-key>V</button>
        <button @click=onTap class=row-key>B</button>
        <button @click=onTap class=row-key>N</button>
        <button @click=onTap class=row-key>M</button>
        <button @click=onBackspace class=row-key>⬅</button>
      </div>
    </div>
  </div>

  <input id=hiddenfield autofocus maxlength=5 @keyup="onKeyup" unselectable="on" onselectstart="return false" />
</template>

<script>

export default {
  name: 'KeyboardGrid',
  props: { },
  emits: ["guess", "update"],
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
        console.log("bogus key", event.key, event.keyCode);
        return;
      }
      if (this.currentGuess.length == 5) {
        return;
      }

      this._didType(event.key);
    },
    _didTypeBackspace() {
      this.currentGuess = this.currentGuess.slice(0, -1);
      this.$emit("update", this.currentGuess);
    },
    _didTypeReturn() {
      if (this.currentGuess.length != 5) {
        return;
      }

      this.$emit("guess", this.currentGuess);
      this.currentGuess = "";
      document.getElementById("hiddenfield").value = "";
    },
    _didType(letter) {
      this.currentGuess += letter;
      this.$emit("update", this.currentGuess);
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

</style>
