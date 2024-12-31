<template>
  <div>
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
import TaskCard from './TaskCard.vue'

const props = defineProps({
  tasks: Array
})

const emit = defineEmits()

function deleteTask(taskId) {
  emit('delete-task', taskId)
}

function toggleComplete(taskId) {
  emit('toggle-complete', taskId)
}
</script>

<style scoped>
div {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
</style>
