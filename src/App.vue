<template>
  <div id="app">
  <TodoContainer/>
  </div>
</template>

<script>
import TodoContainer from './components/TodoContainer.vue'

export default {
  name: 'App',
  components: {
    TodoContainer
  }
}
</script>

<style>
body {
  background: rgb(44, 44, 44);
}
#app {
  display: flex;
  text-align: center;
}
</style>
