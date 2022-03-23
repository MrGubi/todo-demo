<template>
  <div id="app">
    <AddTask @add-task-event="addTask"/>
    <select v-model="sortAfter">
      <option value="uncompleted">Uncompleted</option>
      <option value="deadline">Deadline</option> 
      <option value="priority">Priority</option> 
    </select>
    <TodoContainer v-bind:tasks="tasks" @toggle-task-event="toggleComplete" @delete-task-event="deleteTask"/>
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
            sortAfter: 'uncompleted',
            tasks: [
                {
                    id: 1,
                    title: "This tasks is less important",
                    priority: 1,
                    deadline: "23-03-2023",
                    completed: false,
                },
                {
                    id: 2,
                    title: "This tasks is IMPORTANT",
                    priority: 2,
                    deadline: "25-05-2022",
                    completed: true,
                },
                {
                    id: 3,
                    title: "This tasks is less important",
                    priority: 3,
                    deadline: "25-03-2023",
                    completed: false,
                },
                {
                    id: 4,
                    title: "This tasks is IMPORTANT",
                    priority: 4,
                    deadline: "25-03-2023",
                    completed: true,
                },
                {
                    id: 5,
                    title: "This tasks is less important",
                    priority: 1,
                    deadline: "25-03-2023",
                    completed: false,
                },
                {
                    id: 6,
                    title: "This tasks is IMPORTANT",
                    priority: 2,
                    deadline: "25-05-2022",
                    completed: true,
                },
                {
                    id: 7,
                    title: "This tasks is less important",
                    priority: 3,
                    deadline: "25-03-2023",
                    completed: false,
                },
                {
                    id: 8,
                    title: "This tasks is IMPORTANT",
                    priority: 4,
                    deadline: "25-05-2022",
                    completed: true,
                },
            ]  
        }
    },
  methods: {
    addTask(newTask) {
      this.tasks = [...this.tasks, newTask];
    },
    deleteTask(TaskId){
      this.tasks = this.tasks.filter(task => task.id !== TaskId)
    },
    toggleComplete(TaskId) {
      this.tasks.forEach(element => {
        if(element.id == TaskId)
          element.completed = !element.completed;
      });
      this.sort(this.sortAfter);
    },

    sort: function(sortAfter) {
      function compare(a, b) {
        if(sortAfter == "priority"){
          if (a.priority > b.priority)
            return -1;
          if (a.priority < b.priority)
            return 1;
          return 0;
        }

        if(sortAfter == "deadline"){
          if (a.deadline > b.deadline)
            return 1;
          if (a.deadline < b.deadline)
            return -1;
          if (a.deadline == b.deadline){
            if (a.priority > b.priority)
              return -1;
            if (a.priority < b.priority)
              return 1;
            return 0;
          }
        }

        if(sortAfter == "uncompleted"){
          if (a.completed > b.completed)
            return 1;
          else if (a.completed < b.completed)
            return -1;
          else if (a.completed === b.completed){
            if (a.priority > b.priority)
              return -1;
             if (a.priority < b.priority)
              return 1;
            return 0;
          }
        }
      }
    this.tasks.sort(compare);
    }
  },

  mounted: function() {
    this.sort(this.sortAfter);
  },
  
  watch: {
    tasks(){
      this.sort(this.sortAfter);
    },
    sortAfter(){
      this.sort(this.sortAfter);
    }
  },
}
</script>

<style>
body {
  background: rgb(44, 44, 44);
}
#app {
  display: grid;
  text-align: center;
}
</style>
