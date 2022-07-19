<template>
  <div class=row>
    <div class=row-item>{{ itemForIndex(0) }}</div>
    <div class=row-item>{{ itemForIndex(1) }}</div>
    <div class=row-item>{{ itemForIndex(2) }}</div>
    <div class=row-item>{{ itemForIndex(3) }}</div>
    <div class=row-item>{{ itemForIndex(4) }}</div>
  </div>
</template>

<script>

export default {
  name: 'GridRow',
  props: {
    input: { type: String, default: () => "" },
  },
  methods: {
    itemForIndex: function(index) {
      return this.input[index];
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
