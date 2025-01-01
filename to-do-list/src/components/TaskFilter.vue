<template>
  <div class="task-filter">
    <!-- Поле за въвеждане на текст за филтриране на задачите -->
    <input
        v-model="filterText"
        type="text"
        placeholder="Filter by Task Name"
        @input="filterTasks"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue' // Импортиране на ref за реактивна променлива

// Реактивна променлива за текста на филтъра
const filterText = ref('')

// Дефиниране на емисиите за изпращане на събития към родителя
const emit = defineEmits()

// Функция за обработка на въвеждане в полето за филтър
function filterTasks() {
  emit('filter-task', filterText.value) // Емисия на 'filter-task' със стойността на филтъра
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
