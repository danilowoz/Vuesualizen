<template>
  <div class="list">
    <div class="list-item" v-for="(item, index) in items">
      <span>
        <img :src="item.image" />
        <Btn :func="edit" :index="index" :text="'Editar'" :type="'default'"></Btn>
        <Btn :func="remove" :index="index" :text="'Remover'" :type="'error'"></Btn>
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
import Btn from '@/components/shared/Btn';

export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
    remove: {
      type: Function,
      required: true,
    },
    edit: {
      type: Function,
      required: true,
    },
  },
  components: { Btn },
};
</script>

<style scoped lang="scss">
  .list {
    padding-bottom: 20px;
  }
  .list-item {
    background: #fafafa;
    margin: 0 -20px;
    border-top: 1px solid #eee;
    text-align: left;
    padding: 15px 20px;
    display: flex;
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

</style>
