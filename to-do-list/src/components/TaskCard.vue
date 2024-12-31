<template>
  <div class="task-list">
    <div 
      v-for="task in tasks" 
      :key="task.id" 
      class="task-card" 
      :class="{ completed: task.completed }"
    >
      <div class="task-content">
        <h3>{{ task.name }}</h3>
        <p>{{ task.description }}</p>
      </div>
      <div class="task-actions">
        <button @click="toggleTaskComplete(task.id)">
          {{ task.completed ? 'Uncheck' : 'Check' }}
        </button>
        <button @click="deleteTask(task.id)">Delete</button>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  tasks: Array
})

const emit = defineEmits()

function toggleTaskComplete(taskId) {
  emit('toggle-complete', taskId)
}

function deleteTask(taskId) {
  emit('delete-task', taskId)
}
</script>

<style scoped>
.task-list {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.task-card {
  background-color: #fff;
  padding: 20px;
  margin: 10px;
  width: 100%;
  max-width: 400px;
  border: 1px solid #ccc;
  border-radius: 8px;
  display: flex;
  justify-content: space-between;
  color: #333; 
}

.task-card.completed {
  background-color: #c8e6c9; 
  color: #388e3c; 
}

.task-content h3 {
  font-weight: bold;
  margin: 0;
}

.task-content p {
  font-size: 14px;
  margin: 5px 0;
}

.task-actions button {
  margin-left: 10px;
  padding: 5px 10px;
  cursor: pointer;
}

.task-actions button:hover {
  background-color: #ddd;
}

.task-actions button:focus {
  outline: none;
  box-shadow: 0 0 5px 2px rgba(0, 0, 0, 0.2);
}
</style>
