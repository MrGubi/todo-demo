<template>
  <div id="app">
    <TodoContainer v-bind:tasks="tasks"/>
    <AddTask @add-task-event="addTask"/>
  </div>
</template>

<script>
import TodoContainer from './components/TodoContainer.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    TodoContainer,
    AddTask
  },
  data() {
        return {
            tasks: [
                {
                    id: 1,
                    title: "This tasks is IMPORTANT",
                    priority: 5,
                    deadline: '23.03.2022',
                    completed: false,
                },
                {
                    id: 2,
                    title: "This tasks is less important",
                    priority: 3,
                    deadline: '23.03.2023',
                    completed: false,
                },
            ]  
        }
    },
  methods: {
    addTask(newTask) {
      this.tasks = [...this.tasks, newTask];
    }
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
