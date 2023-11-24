<template>
  <div>
    <p>{{ task.name }}</p>
    <button @click="completeTask">Complete Task</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      task: {
        id: 1,
        name: 'Example Task',
      },
    };
  },
  methods: {
    completeTask() {
      // Ensure that this.onComplete is a function
      if (typeof this.onComplete === 'function') {
        // Call the onComplete method with the task as an argument
        this.onComplete(this.task);
      } else {
        console.error('onComplete is not a function');
      }
    },
  },
};
</script>
