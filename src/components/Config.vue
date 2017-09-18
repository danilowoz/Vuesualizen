<template>
  <div v-bind:class="{ 'edit': edit }" class="config">
    <button class="edit-button" @click="menu">
      <img src='../assets/config.svg' />
    </button>

    <h1>My goals</h1>
    <form action="">
      <div class="image-wrap">
        <label>Image</label>
        <input accept="image/*" placeholder="Paste an url for the image" ref="imagem" type="text">
        <button @click.prevent="add">Add goal</button>
      </div>

      <span>
        <label for="title">Title</label>
        <input placeholder="Small and easy to remember" required ref="title" type="text">

        <label for="time">Deadline</label>
        <input placeholder="A deadline" required ref="time" type="date" />

        <label for="desc">Description<small></small></label>
        <textarea placeholder="Tell with more details" required ref="desc"></textarea>
      </span>

    </form>
    <List :items="items" :remove="remove"></List>
  </div>

</template>

<script>
  import List from '@/components/List';
  
  const localId = 'visualizem';

  export default {
    components: { List },
    props: ['items', 'edit'],
    methods: {
      remove(index) {
        this.items.splice(index, 1);
      },
      add() {
        const title = this.$refs.title.value;
        const desc = this.$refs.desc.value;
        const image = this.$refs.imagem.value;
        const time = this.$refs.time.value;

        if (title !== '' && desc !== '' && image !== '' && time !== '') {
          this.$set(this.items, this.items.length, {
            title,
            desc,
            image,
            time,
          });

          this.cleanInput();
        }
      },
      cleanInput() {
        this.$refs.title.value = '';
        this.$refs.desc.value = '';
        this.$refs.imagem.value = '';
        this.$refs.time.value = '';
      },
      getLocalstorage() {
        const store = JSON.parse(localStorage.getItem(localId));
        return store === null ? [] : store;
      },
      setLocalStorage() {
        localStorage.setItem(localId, JSON.stringify(this.items));
      },
    },
    watch: {
      items() {
        this.setLocalStorage();
      },
    },
    created() {
      this.items = this.getLocalstorage();
    },
  };
</script>

<style scoped>

.config {
  position: fixed;
  top: 0;
  bottom: 0;
  width: 30vw;
  background: #fff;
  z-index: 9999999;
  padding: 20px;
  transition: all .5s ease;
  right: 0;
  transform: translateX(calc(30vw + 40px));
}

.config.edit {
  transform: translateX(0);
}

.config h1 {
  margin: 0;
  color: #a1b323;
  margin-bottom: 30px;
  font-weight: 300;
}

.edit-button {
  display: block;
  width: 35px;
  height: 35px;
  position: absolute;
  left: -70px;
  bottom: 30px;
  background: none;
  border: 0;
  cursor: pointer;
  outline: 0;
  opacity: .4;
  transition: all .3s ease;
}

.config.edit .edit-button,
.edit-button:hover {
  opacity: 1;
}

form {
  padding-bottom: 20px;
  display: flex;
  width: 100%;
}

form span {
  width: 100%;
}

form label {
  display: block;
  margin-top: 10px;
  margin-bottom: 2px;
  font-size: 12px;
}

form label:first-child {
  margin-top: 0;
}

form input,
form textarea {
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

form input:focus,
form textarea:focus{
  outline:none;
  border:1px solid #a1b323;
}

form textarea {
  height: 50px;
}

form .image-wrap {
  width: 100px;
  height: 100px;
  display: block;
  margin-right: 15px;
  padding: 0;
  border-radius: 3px;
  position: relative;
}

form .image-wrap input {
  line-height: 85px;
  width: 100px;
  height: 100px;
  display: block;
}

form button {
  background: #a1b323;
  border: 0;
  color: white;
  border-radius: 3px;
  line-height: 20px;
  width: 100%;
  margin-top: 20px;
  text-align: center;
  transition: all .3s ease;
}

</style>