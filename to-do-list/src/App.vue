<template>
  <div class="app">
    <!-- Основното заглавие на приложението -->
    <h1>To-Do List Manager</h1>

    <!-- Компонент за добавяне на нови задачи -->
    <AddTask @add-task="addTask" />

    <!-- Компонент за филтриране на задачите -->
    <TaskFilter @filter-task="filterTask" />

    <!-- Списък със задачи с предаване на данни и събития -->
    <TaskList
        :tasks="filteredTasks"
        @delete-task="deleteTask"
        @toggle-complete="toggleTaskComplete"
    />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import AddTask from './components/AddTask.vue' // Импортиране на компонент за добавяне на задачи
import TaskFilter from './components/TaskFilter.vue' // Импортиране на компонент за филтриране
import TaskList from './components/TaskCard.vue' // Импортиране на компонент за показване на задачите

// Списък с всички задачи
const tasks = ref([])

// Текстът за филтриране на задачите
const filterText = ref('')

// Функция за добавяне на нова задача
function addTask(newTask) {
  tasks.value.push(newTask) // Добавя новата задача към списъка
}

// Функция за филтриране на задачите по текст
function filterTask(filter) {
  filterText.value = filter // Задава нов филтър
}

// Функция за изтриване на задача по нейното ID
function deleteTask(taskId) {
  tasks.value = tasks.value.filter(task => task.id !== taskId) // Премахва задачата от списъка
}

// Функция за маркиране на задача като завършена/незавършена
function toggleTaskComplete(taskId) {
  const task = tasks.value.find(task => task.id === taskId) // Намира задачата по ID
  if (task) {
    task.completed = !task.completed // Променя състоянието ѝ
  }
}

// Изчислено свойство за филтриране на задачите според текста на филтъра
const filteredTasks = computed(() => {
  return tasks.value.filter(task =>
      task.name.startsWith(filterText.value) // Връща задачите, чиито имена започват с филтъра
  )
})
</script>

<style scoped>
/* Контейнер за приложението */
.app {
  max-width: 600px;
  justify-content: center;
  padding: 20px;
  font-family: 'Arial', sans-serif;
  background-color: #f4f4f4;
  min-height: 100vh;
}

/* Стил за заглавието */
h1 {
  text-align: center;
  color: #333;
}
</style>
