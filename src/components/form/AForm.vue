<template>
  <form class="app__form" ref="fileform">
    <div class="text">ссылка:</div>

    <input type="text" class="text-input" v-model="info.url" />

    <div class="text">или</div>

    <input
      type="file"
      accept=".txt"
      class="file-input"
      @change="chooseFileHandler"
    />

    <input
      type="submit"
      value="добавить"
      name="receive"
      class="submit-input"
      @click.stop="addImage"
    />
  </form>
</template>

<script>
export default {
  name: "AppForm",
  data() {
    return {
      info: {
        url: "",
      },
      json: "",
    };
  },
  methods: {
    addImage(event, json, baseURL) {
      let jsonURLS = json;
      let base = baseURL;

      if (event) {
        event.preventDefault();
      } else if (jsonURLS) {
        this.json = jsonURLS;
        this.$emit("addImage", jsonURLS);
        return;
      } else if (base) {
        this.$emit("addImage", base);
      }

      if (this.info.url != "") {
        this.$emit("addImage", this.info.url);
      } else {
        return;
      }
    },
    chooseFileHandler(event) {
      const file = event.target.files[0];
      const reader = new FileReader();

      reader.onload = (event) => {
        let json = JSON.parse(event.target.result).galleryImages;
        this.addImage(null, json);
      };
      reader.readAsText(file);
    },
  },
};
</script>

<style scoped>
.app__form {
  position: absolute;
  display: flex;
  flex-direction: column;
  max-width: 50%;
  top: 50%;
  left: 50%;
  transform: translateX(-50%) translateY(-50%);
}

.app__form .text-input {
  margin-bottom: 10px;
  padding: 10px;
}

.app__form .text-input:focus {
  border: 1px solid #5c3c92;
}

.app__form .text {
  margin-bottom: 10px;
  font-size: 2em;
  font-weight: 600;
  color: #d72632b9;
}

.app__form .file-input {
  margin-bottom: 20px;
  font-size: 1.1em;
}

.app__form .submit-input {
  margin: 0px auto;
  margin-bottom: 20px;
  padding: 10px;
  font-size: 1.1em;
  background: #fff;
  color: #000;
}

.app__form .submit-input:hover {
  border: 1px solid #5c3c92;
}
</style>
