<!-- components/TaskList.vue -->
<template>
  <div>
    <task v-for="task in tasks" :key="task.id" :task="task" @complete="completeTask" />
  </div>
</template>

<script>
import Task from '~/components/Task.vue';

export default {
  components: {
    Task,
  },
  props: {
    tasks: Array,
    onComplete: Function,
  },
  methods: {
    completeTask(taskId) {
      this.onComplete(taskId);
    },
  },
};
</script>
