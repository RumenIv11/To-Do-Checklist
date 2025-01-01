<template>
  <!-- Форма за добавяне на нова задача -->
  <form @submit.prevent="submitForm" class="add-task-form">
    <!-- Поле за въвеждане на името на задачата -->
    <input
        v-model="taskName"
        type="text"
        placeholder="Task Name"
        required
    />
    <!-- Бутон за потвърждаване на добавянето -->
    <button type="submit">Add Task</button>
  </form>
</template>

<script setup>
import { ref } from 'vue' // Импортиране на ref за реактивни променливи

// Реактивна променлива за съхраняване на името на задачата
const taskName = ref('')

// Емисия за предаване на събития към родителя
const emit = defineEmits()

// Функция за обработка на изпращането на формата
function submitForm() {
  if (taskName.value.trim() !== '') {
    // Емисия на събитие 'add-task' към родителя с данни за новата задача
    emit('add-task', { id: Date.now(), name: taskName.value, completed: false })
    // Изчистване на полето за въвеждане
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
