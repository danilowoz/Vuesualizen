<template>
  <div>
<!--     <div v-for="item in items">
      <h2>{{ item.title }} <small>{{ item.desc }}</small></h2>
      <button @click.prevent="remove">delete</button>
    </div> -->
    {{text}}
  </div>
</template>

<script>

export default {
  data() {
    return {
      text: 'cu',
    };
  },
};
</script>

