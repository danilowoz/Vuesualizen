<template>
  <div class="image-wrap">
    <label class="label-control">Image</label>
    <div class="image-wrap__preview" v-bind:style="{backgroundImage: 'url(' + dataImage + ')'}">
      <input accept="image/*" type="file" ref="file" @change="uploadImage">
    </div>
  </div>
</template>

<script>

export default {
  props: ['getImage', 'updateImage', 'image'],
  data() {
    return {
      dataImage: null,
    };
  },
  methods: {
    uploadImage() {
      const self = this;
      const file = this.$refs.file;
      const reader = new FileReader();
      reader.readAsDataURL(file.files[0]);
      reader.onloadend = function imageLoader(event) {
        self.dataImage = event.target.result;
      };
    },
  },
  watch: {
    dataImage() {
      this.getImage(this.dataImage);
    },
    image() {
      this.dataImage = this.updateImage();
    },
  },
  created() {
    this.dataImage = this.updateImage();
  },
};
</script>

<style scoped lang="scss">
  .label-control {
    display: block;
    margin-bottom: 2px;
    font-size: 12px;
  }

  .image-wrap {
    margin-right: 15px;

    input {
      box-sizing: border-box;
      width: 100px;
      height: 100px;
      display: block;
      border: 1px solid #eee;
      font-family: 'Avenir', Helvetica, Arial, sans-serif;
      line-height: 85px;
      padding: 5px 10px;
    }
  }

  .image-wrap__preview {
    width: 100px;
    height: 100px;
    border-radius: 3px;
    overflow: hidden;
    background-size: cover;
    background-position: center;
  }
</style>