<script setup>
import TodoItem from './TodoItem.vue'
import { ref } from 'vue'

let id = 0
const todos = ref([])
const newTodo = ref('')

function addTodo () {
  if (newTodo.value.length === 0) {
    alert("please fill in a task!");
  } else {
    todos.value.push({ id: id++, text: newTodo.value, done: false, editable: false })
    newTodo.value = ''
  }
}

function saveTodo () {
  // todo.text = newTodo.value
}

function onRemoveTodo (todo) {
  todos.value = todos.value.filter(task => task.id !== todo.id)
}

</script>

<template>
  <div class="greetings">
    <h3>let's keep track of our Todos</h3>
    <div>
      <form @submit.prevent="addTodo">
        <input name="task" v-model="newTodo" />
        <button>submit</button>
      </form>
      <TodoItem
        v-for="(todo, index) in todos"
        :key="index"
        :todo="todo"
        @saveTodo="saveTodo"
        @onRemoveTodo="onRemoveTodo"
      />
    </div>
    
  </div>
</template>

<style scoped>

</style>
