<template>
  <div>
    <h1>Task Manager</h1>

    <div>
      <input v-model="newTask.title" placeholder="Enter task title" />
      <button @click="createTask" :disabled="isNewTaskInvalid">Create Task</button>
    </div>

    <div>
      <h2>Current Tasks</h2>
      <ul>
        <li v-for="task in tasks" :key="task.id">
          {{ task.title }} - {{ task.completed ? 'Completed' : 'Pending' }}
          <button @click="completeTask(task.id)" :disabled="task.completed">Complete</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: { title: '' },
      tasks: [],
    };
  },
  computed: {
    isNewTaskInvalid() {
      return !this.newTask.title.trim();
    },
  },
  methods: {
    async createTask() {
      // Check if the title is not blank before proceeding
      if (this.newTask.title.trim() !== '') {
        // Your logic to create a task...
        const response = await this.$axios.post('/api/tasks', this.newTask);
        this.tasks.push(response.data);
        this.newTask.title = ''; // Clear the input after creating the task
      }
    },
    async completeTask(taskId) {
      // Your logic to mark a task as completed...
      const response = await this.$axios.post(`/api/tasks/${taskId}/complete`);
      const updatedTask = response.data;
      const index = this.tasks.findIndex(task => task.id === updatedTask.id);
      if (index !== -1) {
        this.$set(this.tasks, index, updatedTask);
      }
    },
  },
  async mounted() {
    // Fetch and display existing tasks when the component is mounted
    const response = await this.$axios.get('/api/tasks');
    this.tasks = response.data;
  },
};
</script>

<style scoped>
/* Import the external styles.css file */
@import url('../styles.css');
</style>
