<template>
  <div v-bind:class="{ 'opened': config }" class="config">

    <div v-if="dataItems.length > 0">
      <button class="config-button" @click.prevent="menu">
        <img src='../assets/config.svg' />
      </button>
    </div>

    <div class="content">
      <h1>My goals</h1>
      
      <form action="">
        <div class="image-wrap">
          <label>Image</label>
          <div class="image-wrap__preview" v-bind:style="{backgroundImage: 'url(' + image + ')'}">
            <input accept="image/*" type="file" ref="file" @change="uploadImage">
          </div>
          <Btn :func="add" :text="'Add goal'" :type="'default'"></Btn>
        </div>

        <span>
          <label for="title">Title</label>
          <input placeholder="Small and easy to remember" required type="text" v-model="title">

          <label for="time">Deadline</label>
          <input placeholder="A deadline" required type="date" v-model="time"  />

          <label for="desc">Description<small></small></label>
          <textarea placeholder="Tell with more details" required v-model="desc"></textarea>
        </span>
      </form>

      <List :items="items" :remove="remove" :edit="edit"></List>
    </div>

  </div>

</template>

<script>
  import List from '@/components/List';
  import Btn from '@/components/shared/Btn';

  export default {
    components: { List, Btn },
    props: ['items', 'config', 'menu'],
    data() {
      return {
        dataItems: [],
        image: null,
        title: null,
        time: null,
        desc: null,
      };
    },
    methods: {
      remove(index) {
        this.items.splice(index, 1);
      },
      edit(index) {
        const { image, title, time, desc } = this.dataItems[index];

        this.image = image;
        this.title = title;
        this.time = time;
        this.desc = desc;

        this.remove(index);
      },
      add() {
        const { image, title, time, desc } = this;

        if (title !== null && desc !== null && image !== null && time !== null) {
          this.$set(this.dataItems, this.dataItems.length, {
            title,
            desc,
            image,
            time,
          });

          // clean
          this.image = null;
          this.title = null;
          this.time = null;
          this.desc = null;
        }
      },
      uploadImage() {
        const self = this;
        const file = this.$refs.file;
        const reader = new FileReader();
        reader.readAsDataURL(file.files[0]);
        reader.onloadend = function imageLoader(event) {
          self.image = event.target.result;
        };
      },
    },
    created() {
      this.dataItems = this.items;
    },
  };
</script>

<style scoped lang="scss">
.config {
  position: fixed;
  top: 0;
  bottom: 0;
  width: 30vw;
  background: #fff;
  z-index: 9999999;
  transition: all .5s ease;
  right: 0;
  transform: translateX(calc(30vw + 40px));
  &.opened {
    transform: translateX(0);
  }
  h1 {
    margin: 0;
    color: #a1b323;
    margin-bottom: 30px;
    font-weight: 300;
  }
}

.content {
  padding: 20px 20px 0;
  overflow: scroll;
  height: 100%;
}

.config-button {
  display: block;
  width: 35px;
  height: 35px;
  position: absolute;
  left: -105px;
  bottom: 30px;
  background: none;
  border: 0;
  cursor: pointer;
  outline: 0;
  opacity: .4;
  transition: all .3s ease;
}

.config.opened .config-button, .config-button:hover {
  opacity: 1;
}

form {
  padding-bottom: 20px;
  display: flex;
  width: 100%;
  span {
    width: 100%;
  }
  label {
    display: block;
    margin-top: 10px;
    margin-bottom: 2px;
    font-size: 12px;
    &:first-child {
      margin-top: 0;
    }
  }
  input, textarea {
    border: 1px solid #eee;
    padding: 5px 10px;
    height: 30px;
    border-radius: 3px;
    resize: none;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    width: 100%;
    box-sizing: border-box;
    transition: all .3s ease;
  }
  input:focus {
    outline: none;
    border: 1px solid #a1b323;
  }
  textarea {
    &:focus {
      outline: none;
      border: 1px solid #a1b323;
    }
    height: 50px;
  }
  .image-wrap {
    width: 142px;
    height: 142px;
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
}
</style>