<template>
  <div>
    <div class="list-item" v-for="(item, index) in items">
      <span>
        <img :src="item.image" />
      </span>
      <span>
        <p><span>Title:</span> {{item.title}}</p>
        <p><span>Description:</span> {{item.desc}}</p>
        <button @click.prevent="remove(index)">×</button>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: ['items', 'remove'],
};
</script>

<style scoped>
  .list-item {
    max-width: 600px;
    margin: 0 auto;
    border-bottom: 1px solid #eee;
    text-align: left;
    padding: 15px 0;
    display: flex;
  }
  p {
    line-height: 1.2;
    margin: 0;
  }
  img {
    width: 100px;
    height: auto;
    display: block;
    margin-right: 15px;
  }
</style>