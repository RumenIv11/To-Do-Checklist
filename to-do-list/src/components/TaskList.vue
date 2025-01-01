<template>
  <div>
    <!-- Обхожда списъка със задачи и рендерира компонент TaskCard за всяка -->
    <TaskCard
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @delete-task="deleteTask"
    @toggle-complete="toggleComplete"
    />
  </div>
</template>

<script setup>
import TaskCard from './TaskCard.vue' // Импортира TaskCard компонента

// Дефиниране на пропс tasks, съдържащ масив от задачи
const props = defineProps({
  tasks: Array
})

// Дефиниране на емисиите за комуникация с родителския компонент
const emit = defineEmits()

// Функция за изтриване на задача
function deleteTask(taskId) {
  emit('delete-task', taskId) // Изпраща събитие към родителя с ID на задачата
}

// Функция за промяна на състоянието на задача
function toggleComplete(taskId) {
  emit('toggle-complete', taskId) // Изпраща събитие към родителя с ID на задачата
}
</script>

<style scoped>
div {
  display: flex;
  flex-direction: column;
  gap: 10px; /* Разстояние между компонентите TaskCard */
}
</style>
