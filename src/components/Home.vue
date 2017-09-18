<template>
  <div v-bind:class="{ 'edit': edit }" class="list">

    <Clock class="clock"></Clock>
    <Focus :items="items"></Focus>
    <Config :items="items" :edit="edit"></Config>
    
  </div>
</template>

<script>
import Clock from '@/components/Clock';
import Focus from '@/components/Focus';
import Config from '@/components/Config';

export default {
  name: 'list',
  components: { Clock, Focus, Config },
  data() {
    return {
      items: [],
      edit: false,
    };
  },
  methods: {
    menu() {
      this.edit = !this.edit;
    },
  },
  watch: {
    items() {
      this.edit = this.items.length === 0;
      console.log('items');
    },
  },
  created() {
    console.log(this.items);
    this.edit = this.items.length === 0;
  },
};
</script>

<style scoped>

.list.edit:before {
  content: "";
  background: #a1b323;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 9999999;
  opacity: .7;
}

</style>
