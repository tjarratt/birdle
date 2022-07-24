<template>
  <div class=row>
    <div class=row-item>{{ characterAtIndex(0) }}</div>
    <div class=row-item>{{ characterAtIndex(1) }}</div>
    <div class=row-item>{{ characterAtIndex(2) }}</div>
    <div class=row-item>{{ characterAtIndex(3) }}</div>
    <div class=row-item>{{ characterAtIndex(4) }}</div>
  </div>
</template>

<script>

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
  name: 'GridRow',
  props: {
    input: { type: Array, default: emptyState() },
  },
  methods: {
    characterAtIndex: function(index) {
      return this.input[index].value;
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
  
  text-transform: uppercase;

  width: 2em;
  height: 2em;
  border: 2px solid #3A3A3C;
  padding: 0;

  font-size: 2em;
  font-weight: bold;
  line-height: 2em;
}

</style>
