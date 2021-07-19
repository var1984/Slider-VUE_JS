<template>
  <div v-show='visibleSlide === idx'>
    <slot> </slot>
  </div>
</template>

<script>
export default {
  name: "SliderItems",
  props:['visibleSlide', 'idx']
};
</script>

<style scoped>
img {
   width: 1200px;
  height: 500px;
}
</style>
