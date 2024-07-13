<template>
  <div>
    <li :class="{ completed: todo.complete }">
      <div>
        <input type="checkbox" class="toggle" v-model="isTodoCompleted"/>
        <label for=""> {{ todo.title }}</label>
        <button 
        class="destroy" 
        @click="emit('delete-todo', props.todo)"
        ></button>
        </div>
        </li>
    
  </div>
</template>

<script setup lang="ts">
import type { Todo } from '@/@types'
import { ref, computed, watch } from 'vue';

const props = defineProps<{
  todo: Todo
}>();

const emit = defineEmits<{
  (e: 'delete-todo', todo: Todo): void
  (e: 'update-todo', todo: Todo, completeVal: boolean): void
}>();

const isTodoCompleted = ref<boolean>(props.todo.complete);

watch(() => isTodoCompleted.value, (newVal) => {
  emit("update-todo", props.todo, newVal)
})


// const isTodoCompleted = computed({
//   get: () => props.todo.complete, //sa valeur initiale dépend de props.todo.complete
//   set: (newVal) => emit("update-todo", props.todo, newVal)
// });


</script>

<style scoped></style>
