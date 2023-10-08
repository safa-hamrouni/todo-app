<script setup>
import TodoItem from './TodoItem.vue'
import { ref } from 'vue'

const localStorage = window.localStorage

let id = 0
const todos = ref(JSON.parse(localStorage.getItem('todos')) || [])
const newTodo = ref('')

function addTodo () {
  if (newTodo.value.length === 0) {
    alert("please fill in a task!");
  } else {
    todos.value.push({ 
      id: id++,
      text: newTodo.value,
      done: false,
      editable: false
    })
    localStorage.setItem('todos', JSON.stringify(todos.value))
    newTodo.value = ''
  }
}

function updateTodo (todo) {
  todos.value.push({
    id: todo.id,
    text: todo.text,
    done: todo.done,
    editable: todo.editable
  })
  localStorage.setItem('todos', JSON.stringify(todos.value))
}

function onRemoveTodo (todo) {
  todos.value = todos.value.filter(task => task.id !== todo.id)
  localStorage.setItem('todos', JSON.stringify(todos.value))
}

function markAsDone (todo) {
  const markedTodos = todos.value.map(task => {
    if (task.id === todo.id && !todo.done) {
      task.done = true
    }
    return task
  })
  localStorage.setItem('todos', JSON.stringify(markedTodos))  
}

</script>

<template>
  <div class="greetings">
    <h3>let's keep track of our Todos !!</h3>
    <div>
      <form @submit.prevent="addTodo">
        <input v-model="newTodo" />
        <button>submit</button>
      </form>
      <TodoItem
        v-for="(todo, index) in todos"
        :key="index"
        :todo="todo"
        @saveTodo="saveTodo"
        @onRemoveTodo="onRemoveTodo"
        @markAsDone="markAsDone"
        @updateTodo="updateTodo(todo)"
      />
    </div>
    
  </div>
</template>

<style scoped>

</style>
