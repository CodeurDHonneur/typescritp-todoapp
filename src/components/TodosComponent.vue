<template>
  <div>
    <!-- Header -->
    <TodoHeader @add-todo="addTodo" />
    <!-- Main -->
    <TodoMain
      :todos="todos"
      @delete-todo="deleteTodo"
      @update-todo="updateTodo"
      @edit-todo="editTodo"
    />

    <!-- Footer -->
    <TodoFooter :todos="todos" />
  </div>
</template>

<script setup lang="ts">
import TodoHeader from '@/components/TodoHeader.vue'
import TodoMain from '@/components/TodoMain.vue'
import TodoFooter from '@/components/TodoFooter.vue'
import type { Todo } from '@/@types'
import { ref } from 'vue'
import { nanoid } from 'nanoid'

const todos = ref<Todo[]>([])

function addTodo(value: string): void {
  todos.value.push({
    id: nanoid(),
    title: value,
    complete: false
  })
}

function deleteTodo(todo: Todo): void {
  todos.value = todos.value.filter((t) => t !== todo)
}

function updateTodo(todo: Todo, completedValue: boolean) {
  todo.complete = completedValue
}

function editTodo(todo: Todo, editText: string) {
  todo.title = editText
}
</script>

<style scoped></style>
