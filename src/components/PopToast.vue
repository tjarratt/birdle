<template>
  <div id=toast :class="{faded: fade}">{{ message }}</div>
</template>

<script>

export default {
  name: 'PopToast',
  components: {},
  emits: ['faded'],
  props: ['message'],
  data: function() {
    return {
      fade: false,
    };
  },
  mounted: function() {
    console.log("before");
    window.setTimeout(function() { 
      this.fade = true;
      window.setTimeout(function () { this.$emit("faded"); }.bind(this), 1000);
    }.bind(this), 1000);
  },
}

</script> 

<style scoped>
#toast {
  z-index: 1000;
  position: absolute;
  top: 75px;
  left: 50%;
  pointer-events: none;
  width: fit-content;
  transform: translate(-50%, 0);
  border: none;
  border-radius: 4px;
  padding: 13px;

  font-weight: 700;
  font-size: 14px;
  line-height: 16px;

  background-color: #FFFFFF;

  opacity: 1;
}

#toast.faded  {
  transition: all 1s;
  opacity: 0;
}
</style>
