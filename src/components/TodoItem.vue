<template>
  <li :class="{ completed: todo.complete, editing: editing }">
    <div class="view">
      <input type="checkbox" class="toggle" v-model="isTodoCompleted" />
      <label @dblclick="startEditing"> {{ todo.title }}</label>
      <button class="destroy" @click="emit('delete-todo', props.todo)"></button>
    </div>

    <div class="input-container">
      <input
        type="text"
        id="edit-to-input"
        class="edit"
        v-model="editInput"
        @keyup.enter="finishEdit"
        @blur="cancelEdit"
      />
      <label for="edit-to-input" class="hidden">Editer</label>
    </div>
  </li>
</template>

<script setup lang="ts">
import type { Todo } from '@/@types'
import { ref, computed, watch } from 'vue'

const props = defineProps<{
  todo: Todo
}>()

const emit = defineEmits<{
  (e: 'delete-todo', todo: Todo): void
  (e: 'update-todo', todo: Todo, completeVal: boolean): void
  (e: 'edit-todo', todo: Todo, value: string): void
}>()

const isTodoCompleted = ref<boolean>(props.todo.complete)

watch(
  () => isTodoCompleted.value,
  (newVal) => {
    emit('update-todo', props.todo, newVal)
  }
)

const editText = ref<string>('')

const editInput = computed({
  get: () => props.todo.title,
  set: (val) => {
    editText.value = val
  }
})

const editing = ref<boolean>(false)

function startEditing() {
  editing.value = true
}

function finishEdit() {
  editing.value = false
  editTodo()
}

function editTodo() {
  emit('edit-todo', props.todo, editText.value)
  editText.value = ''
}

function cancelEdit() {
  console.log('cancel edit')
}
// const isTodoCompleted = computed({
//   get: () => props.todo.complete, //sa valeur initiale dépend de props.todo.complete
//   set: (newVal) => emit("update-todo", props.todo, newVal)
// });
</script>

<style scoped></style>
