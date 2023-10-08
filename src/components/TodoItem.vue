<script setup>


const props = defineProps({
  todo: Object
})
</script>

<template>
  <div class="todo-item">
    <input type="checkbox" :checked="todo.done"/>
    <span class="todo-task">{{ todo.text }}</span>
    <button>x</button>   
  </div>
</template>

<style lang="scss" scoped>
.todo {
  &-item {
  // display: flex;
  list-style-type: none;
  }
  &-task {
    min-width: 100px;
    padding-left: 5px;
    padding-right: 5px;
  }
}
</style>