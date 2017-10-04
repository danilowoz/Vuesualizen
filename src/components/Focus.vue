<template>
  <div v-if="itemSelected">
    <div class="image" v-bind:style="{backgroundImage: 'url(' + itemSelected.image + ')'}">
      <div class="content">
        <span>
          <h1>{{itemSelected.title}} <small>until {{itemSelected.time | moment("MMMM Do YYYY")}}</small></h1>
          <p>{{itemSelected.desc}}</p>
        </span>
        <div v-if="counter" class="counter"></div>
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
        counter: false,
      };
    },
    methods: {
      sorterItems() {
        this.counter = false;
        let resultItem = [];

        if (this.items && this.items.length > 0) {
          resultItem = this.items[Math.floor(Math.random() * this.items.length)];

          if (this.itemSelected === resultItem) {
            this.sorterItems();
          } else {
            this.itemSelected = resultItem;
            setTimeout(() => {
              this.counter = true;
            }, 1);
          }
        }

        return false;
      },
    },
    created() {
      this.sorterItems();
      setInterval(() => {
        this.sorterItems();
      }, 10000);
    },
    watch: {
      items() {
        this.sorterItems();
      },
    },
  };
</script>

<style scoped lang="scss">
  $velocityCounter: 10000ms;

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
      animation: slideLeft 1s .5s ease forwards;
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
      animation: slideLeft 1s .7s ease forwards;
      transform: translateX(-20px);
      opacity: 0;
    }
  }

  .counter {
    display: block;
    margin: 0 40px;
    position: absolute;
    left: 0;
    bottom: 20px;
    width: calc(100% - 80px);
    &:before {
      content: "";
      position: absolute;
      left: 0;
      top: 0;
      width: 100%;
      border-bottom: 1px solid #fff;
      opacity: .1;
    }
    &:after {
      content: "";
      position: absolute;
      left: 0;
      top: 0;
      border-bottom: 1px solid #fff;
      opacity: .3;
      width: 100%;
      animation: counter $velocityCounter linear;
      transform-origin: left center;
    }
  }
  
  @keyframes counter {
    0% {
      transform: scale(0,1)
    }
    100% {
      transform: scale(1,1)
    }
  }
</style>