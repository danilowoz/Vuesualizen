<template>
  <div>
    {{hour}}:{{minutes}}
  </div>
</template>

<script>
  export default {
    data() {
      return {
        hour: new Date().getHours(),
        minutes: new Date().getMinutes(),
      };
    },
    methods: {
      updateHour() {
        setInterval(() => {
          if (this.hour !== new Date().getHours()) {
            this.hour = new Date().getHours();
          }
        }, 100);
      },
      updateMinutes() {
        setInterval(() => {
          if (this.minutes !== new Date().getMinutes()) {
            this.minutes = new Date().getMinutes();
          }
        }, 100);
      },
    },
    created() {
      this.updateHour();
      this.updateMinutes();
    },
  };
</script>

<style scoped>
  div {
    font-size: 40px;
    font-weight: lighter;
    color: #fff;
    background: linear-gradient(to bottom, rgba(0,0,0,.8) 0%,rgba(0,0,0,0) 100%);
    position: absolute;
    z-index: 9999;
    padding: 30px;
    padding-bottom: 200px;
    top: 0;
    left: 0;
    right: 0;
  }
</style>