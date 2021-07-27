<template>
  <div id="app">
    <AppForm v-if="!galleryIsChanged" @addImage="addImageHandler" />
    <AGallery
      v-else
      @showChangeGalleryWindow="showChangeGalleryWindowHandler"
      :urls="urls"
      @deleteImage="deleteImageHandler"
    />
  </div>
</template>

<script>
import AppForm from "./components/form/AForm.vue";
import AGallery from "./components/gallery/AGallery.vue";

export default {
  name: "App",
  data() {
    return {
      galleryIsChanged: true,
      urls: [
        "https://upload.wikimedia.org/wikipedia/commons/thumb/a/a1/Johnrogershousemay2020.webp/1200px-Johnrogershousemay2020.webp.png",
        "https://www.industrialempathy.com/img/remote/ZiClJf-1920w.jpg",
        "https://docs.microsoft.com/ru-ru/windows/apps/design/controls/images/image-licorice.jpg",
        "https://im0-tub-ru.yandex.net/i?id=84dbd50839c3d640ebfc0de20994c30d&n=27&h=480&w=480",
        "https://interactive-examples.mdn.mozilla.net/media/cc0-images/grapefruit-slice-332-332.jpg",
        "https://hatrabbits.com/wp-content/uploads/2017/01/random.jpg",
        "https://static.remove.bg/remove-bg-web/3661dd45c31a4ff23941855a7e4cedbbf6973643/assets/start-0e837dcc57769db2306d8d659f53555feb500b3c5d456879b9c843d1872e7baa.jpg",
        "https://helpx.adobe.com/content/dam/help/en/photoshop/using/convert-color-image-black-white/jcr_content/main-pars/before_and_after/image-before/Landscape-Color.jpg",
        "https://upload.wikimedia.org/wikipedia/commons/thumb/b/b6/Image_created_with_a_mobile_phone.png/1200px-Image_created_with_a_mobile_phone.png",
        "https://images.ctfassets.net/hrltx12pl8hq/7yQR5uJhwEkRfjwMFJ7bUK/dc52a0913e8ff8b5c276177890eb0129/offset_comp_772626-opt.jpg?fit=fill&w=800&h=300",
        "https://www.industrialempathy.com/img/remote/ZiClJf-1920w.jpg",
      ],
    };
  },
  methods: {
    addImageHandler(url) {
      try {
        if (Array.isArray(url)) {
          for (let item of url) {
            this.urls.push(item.url);
          }
        } else if (url) {
          console.log("url: ", url);
          this.urls.push(url);
        } else {
          this.urls.push(url);
        }

        this.galleryIsChanged = true;
        localStorage.setItem("urls", JSON.stringify(this.urls));
      } catch (err) {
        console.log(err);
        alert("Не удалось получить");
      }
    },
    deleteImageHandler(index) {
      this.urls.splice(index, 1);
      localStorage.setItem("urls", JSON.stringify(this.urls));
    },
    showChangeGalleryWindowHandler() {
      this.galleryIsChanged = false;
    },
  },
  created() {
    if (localStorage.getItem("urls")) {
      this.urls = JSON.parse(localStorage.getItem("urls"));
    }
  },
  components: {
    AppForm,
    AGallery,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Cinzel:wght@400;500;700&display=swap");

* {
  margin: 0px;
  padding: 0px;
}

body {
  background: #a2d5c6;
}

input,
button {
  box-sizing: border-box;
  outline: none;
  border: 1px solid transparent;
}

input[type="submit"]:hover,
button:hover {
  cursor: pointer;
}

#app {
  position: relative;
  min-height: 100vh;
  padding: 30px;
  padding-top: 80px;
  text-align: center;
  font-size: 14px;
  font-family: "Cinzel", serif;
}
</style>
