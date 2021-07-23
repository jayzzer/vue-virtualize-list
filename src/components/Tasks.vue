<template>
  <div class="tasks">
    <List class="task-list" :items="tasks"/>
  </div>
</template>

<script>
import List from '@/components/List.vue';

const TASK_COUNT = 100;

export default {
  name: 'Tasks',

  components: { List },

  data() {
    return {
      tasks: [],
    };
  },

  created() {
    for (let i = 0; i < TASK_COUNT; i += 1) {
      this.tasks.push(`Task #${i}`);
    }
  },
};
</script>

<style scoped>
.task-list {
  height: 50vh;
}
</style>
