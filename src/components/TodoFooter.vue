<template>
  <footer class="footer" v-if="todos.length > 0">
    <span class="todo-count">
      <strong>{{ remainig }}</strong> tâche{{ remainig > 1 ? 's' : '' }} restante{{
        remainig > 1 ? 's' : ''
      }}
    </span>
    <ul class="filters">
      <li><router-link to="#">Tous</router-link></li>
      <li><router-link to="#">En cours</router-link></li>
      <li><router-link to="#">Terminés</router-link></li>
    </ul>

    <button class="clear-completed">Eff. tâches terminées</button>
  </footer>
</template>

<script setup lang="ts">
import type { Todo } from '@/@types'
import { computed } from 'vue'

const props = defineProps<{
  todos: Todo[]
}>()

const remainig = computed(() => props.todos.filter((todo) => !todo.complete).length)
</script>

<style scoped></style>
