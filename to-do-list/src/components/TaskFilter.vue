<template>
  <div class="task-filter">
    <input 
      v-model="filterText" 
      type="text" 
      placeholder="Filter by Task Name" 
      @input="filterTasks" 
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'

const filterText = ref('')


const emit = defineEmits()

function filterTasks() {
  emit('filter-task', filterText.value)
}
</script>

<style scoped>
.task-filter {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.task-filter input {
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
</style>
