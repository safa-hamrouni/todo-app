<script setup>
import { ref } from 'vue'

const emit = defineEmits(['saveTodo', 'onRemoveTodo'])
const props = defineProps({
  todo: Object
})
const editable = ref(false)
const editOrSave = ref('edit')

function toggleToEditOrSave (e) {
  editable.value =!editable.value
  editOrSave.value = (editable.value ? 'save' : 'edit')
  if (!editable.value) {
    emit('saveTodo')
  }
}

function onRemoveTodo (todo) {
  emit('onRemoveTodo', todo)
}

function testing () {
  console.log('this works')
}
</script>

<template>
  <div class="todo-item">
    <input
      v-model="todo.done"
      type="checkbox"
    />
    <span
      class="todo-task"
      :class="{ done : todo.done}"
      :contenteditable="editable"
    >{{ todo.text }}
    <input type="hidden" v-model="todo.text" @input="testing">
    </span>
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