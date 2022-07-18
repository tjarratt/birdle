<template>
  <div id=wrapper>
    <div class=grid>
      <div class=row>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
      </div>
      <div class=row>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
      </div>
      <div class=row>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
      </div>
      <div class=row>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
      </div>
      <div class=row>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
      </div>
      <div class=row>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
        <div class=row-item></div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'WordGrid',
  props: { },
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

.row {
  display: grid;
  grid-gap: 5px;
  grid-template-columns: repeat(5, 1fr);
  
}

.row-item {
  display: grid;
  grid-gap: 5px;

  width: 4em;
  height: 4em;
  border: 2px solid #3A3A3C;
}

</style>
