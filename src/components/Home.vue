<template>
  <div class="list">

    <div class="view">
      
    </div>

    <div class="config">
      <h1>My goals</h1>
      <form action="">
        <label for="title">Title</label>
        <input required ref="title" type="text">

        <label for="desc">Description</label>
        <textarea required ref="desc"></textarea>

        <input type="text" placeholder="Imagem">
        <button @click.prevent="add">+</button>

        <button @click.prevent="add">Add</button>
      </form>
    </div>

  </div>
</template>

<script>
const localId = 'visualizem';

export default {
  name: 'list',
  data() {
    return {
      items: [],
    };
  },
  methods: {
    remove(item) {
      this.items.splice(this.items.indexOf(item), 1);
    },
    add() {
      const title = this.$refs.title.value;
      const desc = this.$refs.desc.value;

      if (title !== '' && desc !== '') {
        this.$set(this.items, this.items.length, {
          title,
          desc,
        });
      }

      this.cleanInput();
    },
    cleanInput() {
      this.$refs.title.value = '';
      this.$refs.desc.value = '';
    },
    getLocalstorage() {
      return JSON.parse(localStorage.getItem(localId));
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

</style>
