<template>
  <div v-bind:class="{ 'config': config }" class="main">
    <Clock class="clock"></Clock>
    <Focus :items="items"></Focus>
    <Config :items="items" :config="config" :menu="menu"></Config>
  </div>
</template>

<script>
import Clock from '@/components/Clock';
import Focus from '@/components/Focus';
import Config from '@/components/config/Config';

const localId = 'visualizem';

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
    getLocalstorage() {
      try {
        const store = JSON.parse(localStorage.getItem(localId));
        return Array.isArray(store) ? store : [];
      } catch (e) {
        this.setLocalStorage();
      }

      return false;
    },
    setLocalStorage() {
      localStorage.setItem(localId, JSON.stringify(this.items));
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
    this.items = this.getLocalstorage();
    this.config = this.items.length === 0;
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
