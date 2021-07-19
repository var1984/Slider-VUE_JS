<template>
  <div class="deleteItemWrap">
    <div class="deleteIcon"><img :src="deleteIcon" alt="" @click="deletItem"/></div>
  </div>
</template>

<script>
export default {
  name: "DeleteItem",
  data() {
    return {
      deleteIcon: [require("../assets/Delete-icon.png")],
    };
  },
  methods: {
      deletItem(){
          this.$emit('deletItem', this.deletItem)
      }
  },
};
</script>

<style scoped>
.deleteItemWrap {
  height: 40px;
  width: 100%;
  background-color: #000;
  opacity: 0;
  position: absolute;
  bottom: 0;
  display: flex;
  align-items: center;
}
.deleteIcon {
  margin-left: auto;
  margin-right: 10px;

}
</style>
