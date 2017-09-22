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
    margin-top: 10px;
    margin-bottom: 2px;
    font-size: 12px;
    &:first-child {
      margin-top: 0;
    }
  }

  .image-wrap {
    width: 142px;
    height: 126px;
    display: block;
    margin-right: 15px;
    padding: 0;
    border-radius: 3px;
    position: relative;

    input {
      line-height: 85px;
      width: 100px;
      height: 100px;
      display: block;
      font-family: 'Avenir', Helvetica, Arial, sans-serif;
      border: 1px solid #eee;
      box-sizing: border-box;
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