<template>
  <ul class="list">
    <li v-for="item in items" :key="item" class="list__item">{{ item }}</li>
  </ul>
</template>

<script>
export default {
  name: 'List',

  props: {
    items: {
      type: Array,
      default() {
        return [];
      },
    },
  },
};
</script>

<style scoped>
.list {
  overflow: auto;
  border: solid 2px #6d6d6d;
}
</style>
