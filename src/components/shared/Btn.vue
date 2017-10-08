<template>
  <button :class="type" @click.prevent="func(index)">{{text}}</button>
</template>

<script>
export default {
  props: {
    func: {
      type: Function,
      required: true,
    },
    text: {
      type: String,
      required: true,
    },
    type: {
      type: String,
      default: 'text',
    },
    index: {
      type: Number,
      default: 0,
    },
  },
};
</script>

<style scoped lang="scss">

button {
  transition: all .3s ease;
  cursor: pointer;
  outline: none;
}

.default {
  display: block;
  background: #a1b323;
  border: 0;
  color: white;
  border-radius: 3px;
  line-height: 20px;
  width: 100px;
  margin-top: 10px;
  text-align: center;
  transition: all .3s ease;

  &:hover {
    background: darken(#a1b323, 5%);
  }
}

.error {
  background: #fff;
  border: 1px solid #ddd;
  color: #aaa;
  border-radius: 3px;
  line-height: 20px;
  width: 100px;
  margin-top: 10px;
  text-align: center;

  &:hover {
    background: #b33423;
    border: 1px solid #b33423;
    color: #fff;
  }
}

</style>