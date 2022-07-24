<template>
  <div id=wrapper>
    <div class=grid>
      <GridRow v-for="(guess, index) in guesses" :key="index" :input="guess.input" :invalid="guess.invalid" />
    </div>
  </div>
</template>

<script>

import GridRow from './GridRow.vue'

export default {
  name: 'WordGrid',
  components: {
    GridRow,
  },
  props: ['guesses'],
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
  grid-template-rows: repeat(6, 1fr);
  grid-gap: 5px;
  padding: 10px;
}

</style>
