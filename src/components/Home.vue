<template>
  <div v-bind:class="{ 'edit': edit }" class="list">
    <Clock class="clock"></Clock>
    <Focus :items="items"></Focus>
    <Config :items="items" :edit="edit" :menu="menu"></Config>
  </div>
</template>

<script>
import Clock from '@/components/Clock';
import Focus from '@/components/Focus';
import Config from '@/components/Config';

const localId = 'visualizem';

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
        this.edit = true;
      }
    },
  },
  created() {
    this.items = this.getLocalstorage();
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
  animation: fade .3s ease;
}

@keyframes fade {
  0% {
    opacity: 0;
  }
  100% {
    opacity: .7;
  }
}

</style>
