<template>
  <div>
    <div class="list-item" v-for="(item, index) in items">
      <span>
        <img :src="item.image" />
        <button @click.prevent="remove(index)">Remover</button>
      </span>
      <span>
        <p><span>Title:</span> {{item.title}}</p>
        <p><span>Deadline:</span> {{item.time}}</p>
        <p><span>Description:</span> {{item.desc}}</p>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: ['items', 'remove'],
};
</script>

<style scoped lang="scss">
  .list-item {
    margin: 0 -20px;
    border-top: 1px solid #eee;
    text-align: left;
    padding: 15px 20px;
    display: flex;
    background: #fafafa;
  }

  p {
    line-height: 1.2;
    margin: 0 0 10px;
    span {
      font-size: 12px;
      display: block;
      color: #333;
    }
  }

  img {
    width: 100px;
    height: auto;
    display: block;
    margin-right: 15px;
  }

  button {
    background: #fff;
    border: 1px solid #ddd;
    color: #aaa;
    border-radius: 3px;
    line-height: 20px;
    width: 100px;
    margin-top: 20px;
    text-align: center;
    transition: all .3s ease;
    cursor: pointer;
    outline: none;
    &:hover {
      background: #b33423;
      border: 1px solid #b33423;
      color: #fff;
    }
  }
</style>