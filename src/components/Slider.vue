<template>
  <div class="slider">
    <slot></slot>
    
  </div>
</template>

<script>
export default {
  name: "Slider",
};
</script>

<style scoped>
.slider {
  position: relative;
  width: 1200px;
  height: 500px;
  margin: 0 auto;
  overflow: hidden;
}

</style>
