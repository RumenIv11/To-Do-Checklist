<template>
  <div class="app">
    <h1>To-Do List Manager</h1>
    <AddTask @add-task="addTask" />
    <TaskFilter @filter-task="filterTask" />
    <TaskList 
      :tasks="filteredTasks" 
      @delete-task="deleteTask" 
      @toggle-complete="toggleTaskComplete" 
    />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import AddTask from './components/AddTask.vue'
import TaskFilter from './components/TaskFilter.vue'
import TaskList from './components/TaskCard.vue'

const tasks = ref([]) 
const filterText = ref('') 


function addTask(newTask) {
  tasks.value.push(newTask)
}


function filterTask(filter) {
  filterText.value = filter
}


function deleteTask(taskId) {
  tasks.value = tasks.value.filter(task => task.id !== taskId)
}


function toggleTaskComplete(taskId) {
  const task = tasks.value.find(task => task.id === taskId)
  if (task) {
    task.completed = !task.completed
  }
}


const filteredTasks = computed(() => {
  return tasks.value.filter(task => 
    task.name.startsWith(filterText.value)
  )
})
</script>

<style scoped>
.app {
  padding: 20px;
  font-family: 'Arial', sans-serif;
  background-color: #f4f4f4;
  min-height: 100vh;
}

h1 {
  text-align: center;
  color: #333;
}
</style>
