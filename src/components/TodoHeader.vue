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
    />
  </header>
</template>

<script setup lang="ts"></script>

<style scoped></style>
