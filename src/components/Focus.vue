<template>
  <div v-if="itemSelected">
    <div class="image" v-bind:style="{backgroundImage: 'url(' + itemSelected.image + ')'}">
        
      <button class="refresh" @click.prevent="sorterItems">
        <img src='../assets/refresh.svg' />
      </button>

      <div class="content">
        <span>
          <h1>{{itemSelected.title}} <small>until {{itemSelected.time | moment("MMMM Do YYYY")}}</small></h1>
          <p>{{itemSelected.desc}}</p>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
  import Vue from 'vue';

  Vue.use(require('vue-moment'));

  export default {
    props: ['items'],
    data() {
      return {
        itemSelected: [],
      };
    },
    methods: {
      sorterItems() {
        let resultItem = [];

        if (this.items && this.items.length > 0) {
          resultItem = this.items[Math.floor(Math.random() * this.items.length)];

          if (this.itemSelected === resultItem) {
            this.sorterItems();
          } else {
            this.itemSelected = resultItem;
          }
        }

        return false;
      },
    },
    created() {
      this.sorterItems();
    },
    watch: {
      items() {
        this.sorterItems();
      },
    },
  };
</script>

<style scoped lang="scss">
  .image {
    width: 100vw;
    height: 100vh;
    background-size: cover;
    background-position: center;
    position: relative;
  }

  .content {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    padding: 40px;
    padding-top: 200px;
    color: #fff;
    background: linear-gradient(to bottom, rgba(0, 0, 0, 0) 0%, rgba(0, 0, 0, 0.8) 100%);
    span {
      width: 40%;
      display: block;
    }

    h1 {
      font-weight: bold;
      font-size: 22px;
      margin: 0;
      margin-bottom: 5px;
      position: relative;
      animation: slideLeft 1s .4s ease forwards;
      transform: translateX(-20px);
      opacity: 0;
    }

    small {
      opacity: .9;
      font-weight: normal;
      font-size: .8em;
    }

    p {
      margin: 0;
      opacity: .7;
      font-size: 14px;
      animation: slideLeft 1s .6s ease forwards;
      transform: translateX(-20px);
      opacity: 0;
    }
  }

  .refresh {
    display: block;
    width: 30px;
    height: 30px;
    position: absolute;
    right: 30px;
    top: 30px;
    background: none;
    border: 0;
    cursor: pointer;
    outline: 0;
    opacity: .2;
    transition: all .3s ease;
    z-index: 999999;
    &:hover {
      opacity: 1;
    }
  }
  
</style>