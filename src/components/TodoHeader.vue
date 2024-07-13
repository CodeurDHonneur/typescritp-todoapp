<template>
  <header class="header">
    <RouterLink to="/">
      <h1>todos</h1>
    </RouterLink>

    <input
      type="text"
      placeholder="Entrez une tâche"
      class="new-todo"
      autofocus
      autocomplete="off"
      @keyup.enter="
        emit('add-todo', ($event.target as HTMLInputElement).value)
        ;($event.target as HTMLInputElement).value = ''
      "
    />
  </header>
</template>

<script setup lang="ts">
const emit = defineEmits<{
  (e: 'add-todo', value: string): void
}>()
</script>

<style scoped></style>
