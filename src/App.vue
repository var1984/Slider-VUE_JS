<template>
  <div id="app">
    <Slider>
      <SliderItems
        v-for="(slide, idx) of curentPage"
        :key="slide"
        :idx="idx"
        :visibleSlide="visibleSlide"
      >
        <img :src="slide" />
      </SliderItems>
    </Slider>

    <SliderIcons>
      <ul class="SliderIcons">
        <li
          class="icons"
          v-for="(slideIcon, indexIcon) of curentPage"
          :key="indexIcon"
          @click="iconBtn(indexIcon)"
          :class="{ active: indexIcon === visibleSlide ? false : true }"
        >
          <img :src="slideIcon" />
          <DeleteItem @deletItem="deletItem(slideIcon)"/>
        </li>
      </ul>
    </SliderIcons>

    <button class="prev" @click="prev" :disabled="disibledBtnPrev">
      <img :src="arrow.arrowLeft" />
    </button>
    <button class="next" @click="next" :disabled="disibledBtnNext">
      <img :src="arrow.arrowRight" />
    </button>
    <Pagin
      :arrow="arrow"
      :slides="slides"
      @newPage="newPage"
      @activItemOnPage="activItemOnPage"
      
    ></Pagin>
    <UploadFile @items="newItems" @uploadRandomFlick="uploadRandomFlick" :curentPage="curentPage"/>
  </div>
</template>

<script>
import Slider from "./components/Slider.vue";
import SliderItems from "./components/SliderItems.vue";
import SliderIcons from "./components/SliderIcons.vue";
import Pagin from "./components/Pagin.vue";
import UploadFile from "./components/UploadFile.vue";
import DeleteItem from "./components/DeleteItem.vue";

export default {
  name: "App",
  components: {
    Slider,
    SliderItems,
    SliderIcons,
    Pagin,
    UploadFile,
    DeleteItem,
  },
  data() {
    return {
      slides: [
        require("./assets/Bubbles.jpg"),
        require("./assets/Forest.jpg"),
        require("./assets/Hubble_Extreme_Deep_Field.jpg"),
        require("./assets/Huntington_bancshares.jpg"),
        require("./assets/Lotus.jpg"),
        require("./assets/Mansion.jpg"),
        require("./assets/Moon.jpg"),
        require("./assets/Three.jpg"),
        require("./assets/Tie_dye.jpg"),
        require("./assets/Vaporwave_wallpaper.jpg"),
      ],
      arrow: {
        arrowLeft: [require("./assets/Arrow-left.png")],
        arrowRight: [require("./assets/Arrow-right.png")],
      },
      visibleSlide: 0,
      curentPage: [],
    };
  },
  methods: {
    next() {
      this.visibleSlide += 1;
    },
    prev() {
      this.visibleSlide -= 1;
    },
    iconBtn(indexIcon) {
      this.visibleSlide = indexIcon;
    },
    newItems(items) {
      let reader = new FileReader();
      reader.readAsDataURL(items);
      reader.onload = () => {
        this.slides.push(reader.result);
      };
      // this.slides.push(URL.createObjectURL (items));
      // console.log(this.slides);
    },
    newPage(newPage) {
      this.curentPage = newPage;
    },
    activItemOnPage(activItemOnPage) {
      this.visibleSlide = activItemOnPage;
    },
    deletItem(slideIcon){
       this.curentPage = this.curentPage.filter(elem => elem !== slideIcon);
       this.slides = this.slides.filter(elem => elem !== slideIcon);
    },
    uploadRandomFlick(uploadRandomFlick){
      this.slides.push(uploadRandomFlick);
      console.log(uploadRandomFlick);
       }
  },
  computed: {
    disibledBtnNext() {
      if (this.visibleSlide === this.visibleSlideLength - 1) return true;
      return false;
    },
    disibledBtnPrev() {
      if (this.visibleSlide === 0) return true;
      return false;
    },
    visibleSlideLength() {
      return [...this.curentPage].length;
    },
  },
};
</script>

<style scoped>
button {
  width: 80px;
  height: 120px;
  border: none;
  background-color: #fff;
  position: absolute;
  top: 250px;
  cursor: pointer;
}
button img {
  width: 100%;
  height: 100%;
}
button:disabled img {
  opacity: 0.2;
}
.next {
  right: 200px;
}
.prev {
  left: 200px;
}
</style>
