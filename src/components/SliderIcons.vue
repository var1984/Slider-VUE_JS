<template>
  <div class="wrap">
   
  <slot></slot>
  </div>
</template>

<script>

export default {
  name: "SliderIcons",
};
</script>

<style scoped>
.wrap {
  margin: auto;
  width: 1200px;
}
.SliderIcons {
  display: flex;
  list-style-type: none;
  justify-content: space-between;
  padding: 0;
}
.icons {
  cursor: pointer;
  position: relative;
  width: 120px;
  height: 120px;
}
.active::before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
}
.icons img {
  width: 100%;
  height: 100%;
}
.icons:hover .deleteItemWrap{
  opacity: 0.5;
}
</style>
