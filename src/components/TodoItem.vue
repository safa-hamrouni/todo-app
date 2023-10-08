<script setup>
import { ref, watch } from 'vue'

const emit = defineEmits([
  'saveTodo',
  'onRemoveTodo',
  'markAsDone',
  'updateTodo'
])
const props = defineProps({
  todo: Object
})
const editable = ref(false)
const editOrSave = ref('edit')

function toggleToEditOrSave (e) {
  if (props.todo.done) {
    alert('this task has been checked, you need to uncheck it to edit')
  } else {
    editable.value = !editable.value
    editOrSave.value = (editable.value ? 'save' : 'edit')
    if (!editable.value) {
      emit('saveTodo')
    }
  }
}

function markAsDone (todo) {
  emit('markAsDone')
}

function onRemoveTodo (todo) {
  emit('onRemoveTodo')
}

function updateTodo (e) {
  emit('updateTodo',)
}

</script>

<template>
  <div class="todo-item">
    <input
      v-model="todo.done"
      type="checkbox"
      @click="markAsDone(todo)"
    />
    <input 
      class="todo-task"
      :class="{ done : todo.done}"
      v-model="todo.text"
      :readonly="!editable"
      @change="updateTodo"
    />
    <button @click="onRemoveTodo(todo)">X</button>
    <button @click="toggleToEditOrSave">{{ editOrSave }}</button>   
  </div>
</template>

<style lang="scss" scoped>
.todo {
  &-item {
    list-style-type: none;
  }
  &-task {
    min-width: 100px;
    padding-left: 5px;
    padding-right: 5px;
  }
}
.done {
  text-decoration: line-through;
} 
</style>