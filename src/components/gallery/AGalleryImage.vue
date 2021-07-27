<template>
  <div class="img">
    <button class="img__button" @click="$emit('deleteImage', index)">
      &#10006;
    </button>
    <img :src="url" />
  </div>
</template>

<script>
export default {
  name: "GalleryImage",
  props: ["url", "index"],
};
</script>

<style>
img {
  height: 100%;
}

.img {
  position: relative;
}

.img__button {
  position: absolute;
  left: 100%;
  transform: translateX(-100%);
  top: 0px;
  width: 25px;
  color: #5c3c92;
  background: #fff;
}

@media all and (max-width: 425px) {
  .img {
    height: 90px;
  }
}

@media all and (min-width: 426px) and (max-width: 768px) {
  .img {
    height: 170px;
  }
}

@media all and (min-width: 427px) and (max-width: 1024px) {
  .img {
    height: 240px;
  }
}

@media all and (min-width: 1025px) and (max-width: 1440px) {
  .img {
    height: 300px;
  }
}

@media all and (min-width: 1441px) {
  .img {
    height: 320px;
  }
}
</style>
