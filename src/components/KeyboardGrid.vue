<template>
  <div id=wrapper>
    <div class=grid>
      <div class=row>
        <button class=row-key>Q</button>
        <button class=row-key>W</button>
        <button class=row-key>E</button>
        <button class=row-key>R</button>
        <button class=row-key>T</button>
        <button class=row-key>Y</button>
        <button class=row-key>U</button>
        <button class=row-key>I</button>
        <button class=row-key>O</button>
        <button class=row-key>P</button>
      </div>
      <div class=row>
        <button class=row-key>A</button>
        <button class=row-key>S</button>
        <button class=row-key>D</button>
        <button class=row-key>F</button>
        <button class=row-key>G</button>
        <button class=row-key>H</button>
        <button class=row-key>J</button>
        <button class=row-key>K</button>
        <button class=row-key>L</button>
      </div>
      <div class=row>
        <button id=key-return class=row-key>ENTER</button>
        <button class=row-key>Z</button>
        <button class=row-key>X</button>
        <button class=row-key>C</button>
        <button class=row-key>V</button>
        <button class=row-key>B</button>
        <button class=row-key>N</button>
        <button class=row-key>M</button>
        <button class=row-key>⬅</button>
      </div>
    </div>
  </div>

  <input autofocus maxlength=5 @keyup="onKeyup" />
</template>

<script>

export default {
  name: 'KeyboardGrid',
  props: { },
  emits: ["guess"],
  data() {
    return {
      currentGuess: "",
    }
  },
  methods: {
    onKeyup: function(event) {
      if (event.keyCode == 13) {
        this.$emit("guess", this.currentGuess);
        this.currentGuess = "";
        return;
      }
      if (event.keyCode == 8) {
        this.currentGuess = this.currentGuess.slice(0, -1);
        return;
      }
      if (event.keyCode < 65 || event.keyCode > 90) {
        console.log("bogus key", event.key, event.keyCode);
        return;
      }

      this.currentGuess += event.key;
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
