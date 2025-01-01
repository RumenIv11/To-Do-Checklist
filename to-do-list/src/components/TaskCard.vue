<template>
  <div class="task-list">
    <!-- Обхожда списъка със задачи и рендерира всяка като карта -->
    <div
        v-for="task in tasks"
        :key="task.id"
        class="task-card"
        :class="{ completed: task.completed}"
    >
    <!-- Съдържание на задачата: име и описание -->
    <div class="task-content">
      <h3>{{ task.name }}</h3>
      <p>{{ task.description }}</p>
    </div>
    <!-- Действия за всяка задача: маркиране като завършена/незавършена и изтриване -->
    <div class="task-actions">
      <button @click="toggleTaskComplete(task.id)">
        {{ task.completed ? 'Uncheck' : 'Check' }} <!-- Текст на бутона според състоянието -->
      </button>
      <button @click="deleteTask(task.id)">Delete</button>
    </div>
  </div>
  </div>
</template>

<script setup>
// Дефиниране на пропс tasks, който съдържа списък със задачи
const props = defineProps({
  tasks: Array // Очаква се tasks да е масив
})

// Дефиниране на емисиите за комуникация с родителския компонент
const emit = defineEmits()

// Функция за маркиране на задача като завършена/незавършена
function toggleTaskComplete(taskId) {
  emit('toggle-complete', taskId) // Изпраща събитие 'toggle-complete' с ID на задачата
}

// Функция за изтриване на задача
function deleteTask(taskId) {
  emit('delete-task', taskId) // Изпраща събитие 'delete-task' с ID на задачата
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
  text-decoration: line-through; /* Подчертава завършените задачи */
  background-color: #c8e6c9; /* Светлозелен фон за завършените задачи */
  color: #388e3c; /* Текст в зелено */
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
  background-color: #ddd; /* Промяна на цвета при задържане на бутона */
}

.task-actions button:focus {
  outline: none;
  box-shadow: 0 0 5px 2px rgba(0, 0, 0, 0.2); /* Подчертаване на бутона при фокус */
}
</style>
