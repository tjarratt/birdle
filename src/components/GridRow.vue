<template>
  <div class=row :class="{shake: invalid}">
    <div class=row-item :class="{correct: isCorrect(0), misplaced: isMisplaced(0)}">{{ characterAtIndex(0) }}</div>
    <div class=row-item :class="{correct: isCorrect(1), misplaced: isMisplaced(1)}">{{ characterAtIndex(1) }}</div>
    <div class=row-item :class="{correct: isCorrect(2), misplaced: isMisplaced(2)}">{{ characterAtIndex(2) }}</div>
    <div class=row-item :class="{correct: isCorrect(3), misplaced: isMisplaced(3)}">{{ characterAtIndex(3) }}</div>
    <div class=row-item :class="{correct: isCorrect(4), misplaced: isMisplaced(4)}">{{ characterAtIndex(4) }}</div>
  </div>
</template>

<script>

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

export default {
  name: 'GridRow',
  props: {
    input: { type: Array, default: emptyState().input },
    invalid:{ type: Boolean, default: emptyState().invalid },
  },
  methods: {
    characterAtIndex: function(index) {
      return this.input[index].value;
    },
    isCorrect: function(index) {
      return this.input[index].state == "correct";
    },
    isMisplaced: function(index) {
      return this.input[index].state == "misplaced";
    },
  },
}

</script> 

<style scoped>

.row {
  display: grid;
  grid-gap: 5px;
  grid-template-columns: repeat(5, 1fr);
  
}

.row-item {
  display: grid;
  grid-gap: 5px;
  box-sizing: border-box;
  justify-content: center;
  align-items: center;
  vertical-align: middle;

  color: white;
  text-transform: uppercase;

  width: 2em;
  height: 2em;
  border: 2px solid #3A3A3C;
  padding: 0;

  font-size: 2em;
  font-weight: bold;
  line-height: 2em;
}

.row-item.correct {
  background-color: #538D4E;
}

.row-item.misplaced {
  background-color: #B29F4C;
}

.shake {
  animation: shake 1s;
}

@keyframes shake {
  0% { transform: translateX(-5px); }

  5% { ransform: translateX(5px); }

  10% { ransform: translateX(-5px); }

  15% { transform: translateX(5px); }

  20% { transform: translateX(-5px); }

  25% { transform: translateX(5px); }

  30% { transform: translateX(-5px); }

  35% { transform: translateX(0); }
}


</style>
