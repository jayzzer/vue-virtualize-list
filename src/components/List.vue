<template>
  <ul class="list">
    <VirtualizedList :items="items" :item-height="18.4">
      <template #default="{ item }">
        <li class="list__item">{{ item }}</li>
      </template>
    </VirtualizedList>
  </ul>
</template>

<script>
import VirtualizedList from '@/components/VirtualizedList.vue';

export default {
  name: 'List',
  components: { VirtualizedList },
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
  border: solid 2px #6d6d6d;
}
</style>
