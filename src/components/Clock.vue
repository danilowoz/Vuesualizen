<template>
  <div class="clock">
    <span>
      {{hour}}:{{minutes}}
    </span>
  </div>
</template>

<script>
  import moment from 'moment';
  
  export default {
    data() {
      return {
        hour: moment().format('h'),
        minutes: moment().format('mm'),
      };
    },
    methods: {
      updateHour() {
        setInterval(() => {
          if (this.hour !== moment().format('h')) {
            this.hour = moment().format('h');
          }
        }, 100);
      },
      updateMinutes() {
        setInterval(() => {
          if (this.minutes !== moment().format('mm')) {
            this.minutes = moment().format('mm');
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

<style scoped lang="scss">
  .clock {
    font-size: 40px;
    font-weight: lighter;
    color: #fff;
    background: linear-gradient(to bottom, rgba(0,0,0,.8) 0%,rgba(0,0,0,0) 100%);
    position: absolute;
    z-index: 9999;
    padding: 40px;
    padding-bottom: 200px;
    top: 0;
    left: 0;
    right: 0;
    span {
      display: block;
      animation: slideLeft 1s .2s ease forwards;
      transform: translateX(-20px);
      opacity: 0;
    }
  }
</style>