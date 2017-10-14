<template>
  <div v-bind:class="{ 'config': config }" class="main">
    <Clock class="clock"></Clock>
    <Focus :items="items"></Focus>
    <Config :items="items" :config="config" :menu="menu" :getData="getData"></Config>
  </div>
</template>

<script>
import localforage from 'localforage';
import Clock from '@/components/Clock';
import Focus from '@/components/Focus';
import Config from '@/components/config/Config';

export default {
  name: 'main',
  components: { Clock, Focus, Config },
  data() {
    return {
      items: [],
      config: false,
    };
  },
  methods: {
    menu() {
      this.config = !this.config;
    },
    getData(value) {
      this.items = value;
    },
    getLocalstorage() {
      return localforage.getItem('items');
    },
    setLocalStorage() {
      localforage.setItem('items', JSON.stringify(this.items));
    },
  },
  watch: {
    items() {
      this.setLocalStorage();
      if (this.items.length === 0) {
        this.config = true;
      }
    },
  },
  created() {
    this.getLocalstorage().then((value) => {
      const store = JSON.parse(value);
      this.items = Array.isArray(store) ? store : [];
      this.config = this.items.length === 0;
    });
  },
};
</script>

<style scoped lang="scss">

.main {
  animation: fade .3s ease;
  
  &.config:before {
    content: "";
    background: #a1b323;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 9999999;
    opacity: .7;
    animation: fade .3s ease;
  }
}

</style>
