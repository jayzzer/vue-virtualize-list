<template>
  <div ref="content" class="content" @scroll="handleScroll">
    <div
      class="content__wrapper"
      :style="wrapperStyles"
    >
      <div
        v-for="item in visibleItems"
        :key="item.index"
        class="content__item"
        :style="`transform: translateY(${item.index * itemHeight}px)`"
      >
        <slot :item="item.value" :index="item.index"></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VirtualizedList',

  props: {
    items: {
      type: Array,
      default() {
        return [];
      },
    },
    itemHeight: {
      type: Number,
      default: 10,
    },
  },

  data() {
    return {
      startIndex: 0,
      endIndex: 0,
    };
  },

  computed: {
    contentRef() {
      return this.$refs.content;
    },
    visibleItems() {
      const itemsToShow = this.items.slice(this.startIndex, this.endIndex + 1);
      return itemsToShow.map((item, index) => ({
        index: index + this.startIndex,
        value: item,
      }));
    },
    wrapperStyles() {
      return `min-height: ${this.items.length * this.itemHeight}px`;
    },
  },

  methods: {
    handleScroll() {
      const { height } = this.contentRef.getBoundingClientRect();
      const { scrollTop } = this.contentRef;

      this.startIndex = Math.max(0, Math.floor(scrollTop / this.itemHeight));
      this.endIndex = Math.floor((scrollTop + height) / this.itemHeight);
    },
  },

  mounted() {
    this.handleScroll();
  },
};
</script>

<style scoped>
.content {
  overflow: auto;
  height: 100%;
}

.content__wrapper {
  position: relative;
}

.content__item {
  position: absolute;
}
</style>
