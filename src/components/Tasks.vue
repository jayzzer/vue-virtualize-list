<template>
  <div class="tasks">
    <input type="number" v-model="tasksCount">
    <List class="task-list" :items="tasks"/>
  </div>
</template>

<script>
import List from '@/components/List.vue';

const DEFAULT_TASK_COUNT = 100;

export default {
  name: 'Tasks',

  components: { List },

  data() {
    return {
      tasksCount: DEFAULT_TASK_COUNT,
      tasks: [],
    };
  },

  watch: {
    tasksCount: {
      immediate: true,
      handler(value) {
        this.tasks = this.generateTasks(value);
      },
    },
  },

  methods: {
    generateTasks(count) {
      const generatedTasks = [];
      for (let i = 0; i < count; i += 1) {
        generatedTasks.push(`Task #${i}`);
      }

      return generatedTasks;
    },
  },
};
</script>

<style scoped>
.task-list {
  height: 50vh;
}
</style>
