<script setup>
import TodoView from './components/TodoView.vue'
</script>

<template>
  <main>
    <div class="wrapper">
      <TodoView msg="You did it!" />
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

@media (min-width: 1024px) {
  main {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }
}
</style>
