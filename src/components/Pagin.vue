<template>
  <div>
    <div class="arrowWrap">
      <button class="prev arrow" @click="pagePrev" :disabled="disibledPagePrev">
        <img :src="arrow.arrowLeft" />
      </button>
      <span> {{ pageNum + 1 }} / {{ numPages }}</span>
      <button class="next arrow" @click="pageNext" :disabled="disibledPageNext">
        <img :src="arrow.arrowRight" />
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Pagin",
  props: {
    arrow: {
      type: Object,
      required: true,
    },
    slides: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      itemsPage: 9,
      pageNum: 0,
    };
  },
  methods: {
    pageNext() {
      this.pageNum += 1;
      this.$emit("newPage", this.newPage);
      this.$emit("activItemOnPage", this.newPage.indexOf(this.newPage[0]));
    },
    pagePrev() {
      this.pageNum -= 1;
      this.$emit("newPage", this.newPage);
      this.$emit("activItemOnPage", this.newPage.indexOf(this.newPage[0]));
    },
  },
  created() {
    this.$emit("newPage", this.newPage);
  },
  computed: {
    startPage() {
      return this.pageNum * this.itemsPage;
    },
    andPage() {
      return this.startPage + this.itemsPage;
    },
    newPage() {
      return this.slides.slice(this.startPage, this.andPage);
    },
    numPages() {
      return Math.ceil(this.slides.length / this.itemsPage);
    },
    disibledPageNext() {
      if (this.pageNum === this.numPages - 1) return true;
      return false;
    },
    disibledPagePrev() {
      if (this.pageNum === 0) return true;
      return false;
    },
  },
};
</script>

<style scoped>
.arrowWrap {
  display: flex;
  justify-content: center;
  margin-top: 45px;
}
.arrow {
  width: 75px;
  height: 75px;
  border: none;
  background-color: #fff;
  cursor: pointer;
}
.arrow img {
  width: 100%;
  height: 100%;
}
span {
  font-size: 70px;
}
button:disabled {
  opacity: 0.2;
}
.next {
  margin-left: 40px;
}
.prev {
  margin-right: 40px;
}
</style>
