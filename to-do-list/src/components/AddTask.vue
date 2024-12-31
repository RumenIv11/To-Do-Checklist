<template>
  <form @submit.prevent="submitForm" class="add-task-form">
    <input 
      v-model="taskName" 
      type="text" 
      placeholder="Task Name" 
      required 
    />
    <button type="submit">Add Task</button>
  </form>
</template>

<script setup>
import { ref } from 'vue'

const taskName = ref('')


const emit = defineEmits()

function submitForm() {
  if (taskName.value.trim() !== '') {
    emit('add-task', { id: Date.now(), name: taskName.value, completed: false })
    taskName.value = ''
  }
}
</script>

<style scoped>
.add-task-form {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.add-task-form input {
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 10px;
}

.add-task-form button {
  padding: 10px 20px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.add-task-form button:hover {
  background-color: #45a049;
}
</style>
