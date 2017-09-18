<template>
  <div class="image" v-bind:style="{backgroundImage: 'url(' + itemFiltered.image + ')'}">
    <div class="content">
      <span>
        <h1>{{itemFiltered.title}} <small>until {{itemFiltered.time | moment("MMMM Do YYYY")}}</small></h1>
        <p>{{itemFiltered.desc}}</p>
      </span>
    </div>
  </div>
</template>

<script>
  import Vue from 'vue';

  Vue.use(require('vue-moment'));

  export default {
    props: ['items'],
    computed: {
      itemFiltered() {
        return this.items[Math.floor(Math.random() * this.items.length)];
      },
    },
  };
</script>

<style scoped>
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
    background: linear-gradient(to bottom, rgba(0,0,0,0) 0%,rgba(0,0,0,.8) 100%);
  }

  .content span {
    width: 40%;
    display: block;
  }

  h1 {
    font-weight: bold;
    font-size: 22px;
    margin: 0;
    margin-bottom: 15px;
  }

  small {
    opacity: .9;
    font-weight: normal;
  }

  p {
    margin: 0;
    opacity: .7;
    font-size: 14px;
  }
</style>