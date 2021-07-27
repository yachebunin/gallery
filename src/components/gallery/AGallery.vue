<template>
  <div class="app__gallery">
    <button @click="$emit('showChangeGalleryWindow')" class="button">
      добавить
    </button>
    <GalleryImage
      v-for="(url, index) in urls"
      :key="index"
      :index="index"
      :url="url"
      @deleteImage="deleteImage"
    />
  </div>
</template>

<script>
import GalleryImage from "./AGalleryImage.vue";

export default {
  name: "App",
  props: ["urls"],
  components: {
    GalleryImage,
  },
  methods: {
    deleteImage(index) {
      this.$emit("deleteImage", index);
    },
  },
};
</script>

<style>
.app__gallery {
  position: relative;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  align-content: flex-start;
}

.app__gallery .button {
  position: absolute;
  top: -60px;
  left: 50%;
  transform: translateX(-50%);
  padding: 10px;
  font-size: 1.1em;
  letter-spacing: 1px;
  color: #5c3c92;
  background: #fff;
  text-transform: uppercase;
}

.app__gallery .button:active,
.app__gallery .img__button:active {
  color: #fff;
  background: #5c3c92;
}
</style>
