<template>
  <main class="main">
    <ul class="todo-list">
      <TodoItem v-for="todo in todos" :key="todo.id" :todo="todo" />
    </ul>
  </main>
</template>

<script setup lang="ts">
import type { Todo } from '@/@types'
import TodoItem from '@/components/TodoItem.vue'

// const props = defineProps(['todos']);
const props = defineProps<{
  todos: Todo[]
}>()
</script>

<style scoped></style>
