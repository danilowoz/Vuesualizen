<template>
  <div class="list">

    <Main :items="items"></Main>

    <div class="config">
      <h1>My goals</h1>
      <form action="">
        <label for="title">Title</label>
        <input required ref="title" type="text">

        <label for="desc">Description</label>
        <textarea required ref="desc"></textarea>

        <input ref="image" type="text" placeholder="Imagem">

        <button @click.prevent="add">Add</button>
      </form>
      <List :items="items" :remove="remove"></List>
    </div>

  </div>
</template>

<script>
import List from '@/components/List';
import Main from '@/components/Main';

const localId = 'visualizem';

export default {
  name: 'list',
  components: { List, Main },
  data() {
    return {
      items: [],
    };
  },
  methods: {
    remove(index) {
      this.items.splice(index, 1);
    },
    add() {
      const title = this.$refs.title.value;
      const desc = this.$refs.desc.value;
      const image = this.$refs.image.value;

      if (title !== '' && desc !== '' && image !== '') {
        this.$set(this.items, this.items.length, {
          title,
          desc,
          image,
        });

        this.cleanInput();
      }
    },
    cleanInput() {
      this.$refs.title.value = '';
      this.$refs.desc.value = '';
      this.$refs.image.value = '';
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
