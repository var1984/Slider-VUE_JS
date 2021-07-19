<template>
  <div class="uploadPage">
    <input type="file" id="uploadFile" @change="previewImg" />
    <label for="uploadFile" class="wrapUpload__Btn btn-style"
      >Upload new image</label
    >
    <button class="uploadFile__Flick-Btn btn-style" @click="uploadFileFlick">
      Upload from Flickr
    </button>
  </div>
</template>

<script>
export default {
  name: "UploadFile",
  props:['newPage'],
  data() {
    return {};
  },
  methods: {
    previewImg(e) {
      this.items = e.target.files[0];
      this.$emit("items", this.items);
    },
    uploadFileFlick() {
      fetch(
        "https://api.flickr.com/services/rest/?method=flickr.photos.search&format=json&nojsoncallback=1&api_key=9c0b191a1d8415714a70a2a3db4abdeb&extras=url_m&text=nature"
      )
        .then((response) => {
          return response.json();
        })
        .then((data) => {
          let items = data.photos.photo;
          let randomItem =
            items[Math.floor(Math.random() * items.length)].url_m;
          // console.log( randomItem);
          return this.$emit("uploadRandomFlick", randomItem);
        });
    },
  },
};
</script>

<style scoped>
#uploadFile {
  width: 0;
  height: 0;
  opacity: 0;
  overflow: hidden;
}
.btn-style {
  font-family: Arial, Helvetica, sans-serif;
  padding: 25px 65px;
  margin-left: 50px;
  background-color: #252525;
  color: #fff;
  border-radius: 40px;
  font-size: 30px;
  border: none;
  cursor: pointer;
}
.btn-style:hover {
  background-color: #464646;
}
.btn-style:active {
  background-color: #111111;
}
.uploadPage {
  margin-top: 45px;
  display: flex;
  justify-content: center;
}
</style>
