<template>
  <div id="app">
  <div class="header">
    <h1 class="Titel">Vue ToDo</h1>
    <button @click="addHidden = !addHidden">+</button>
  </div>
  <div class="addtask" :style="isHidden">
    <AddTask @add-task-event="addTask"/> 
  </div>
    <div class="sort">
      <button value="uncompleted" @click="sortAfter = 'uncompleted'" v-bind:class="{ 'selected' : sortAfter == 'uncompleted' }">Uncompleted</button>
      <button value="deadline" @click="sortAfter = 'deadline'" v-bind:class="{ 'selected' : sortAfter == 'deadline' }">Deadline</button> 
      <button value="priority" @click="sortAfter = 'priority'" v-bind:class="{ 'selected' : sortAfter == 'priority' }">Priority</button> 
    </div>
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
            addHidden: true,
            sortAfter: 'uncompleted',
            tasks: [
                {
                    id: 1,
                    title: "This tasks is less important",
                    priority: 1,
                    deadline: 1648738500000,
                    completed: false,
                },
                {
                    id: 2,
                    title: "This tasks is IMPORTANT",
                    priority: 2,
                    deadline: 1648663200000,
                    completed: true,
                },
                {
                    id: 3,
                    title: "This tasks is and there is not much time left",
                    priority: 3,
                    deadline: 1648738500000,
                    completed: false,
                },
                {
                    id: 4,
                    title: "This tasks is IMPORTANT",
                    priority: 4,
                    deadline: 1648663200000,
                    completed: true,
                },
                {
                    id: 5,
                    title: "This tasks is less important",
                    priority: 1,
                    deadline: 1648663200000,
                    completed: false,
                },
                {
                    id: 6,
                    title: "This tasks is IMPORTANT",
                    priority: 2,
                    deadline: 1648663200000,
                    completed: true,
                },
                {
                    id: 7,
                    title: "This tasks is less important",
                    priority: 3,
                    deadline: 1648663200000,
                    completed: false,
                },
                {
                    id: 8,
                    title: "This tasks is IMPORTANT",
                    priority: 4,
                    deadline: 1648663200000,
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

  computed:{
    isHidden(){
      if(this.addHidden){
        return {'--header-display': 'none'};
      }
      else{
        return {'--header-display': 'show'};
      }
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
    },
  },
}
</script>

<style>
body {
  background: rgb(44, 44, 44);
}
#app {
  margin: auto;
  display: grid;
  text-align: center;
  height: auto;
  width: 25vw;
  overflow-y: hidden;
  background: #fff;
}

#app .sort {
  padding-bottom: 10px;
  padding-left: 10px;
  text-align: left;
  order: 3;
}

#app .sort button{
  height: 30px;
  border-color: #2a89f8;
  border-style: solid;
  border-radius: 5px;
  background: none;
  transition-duration: 100ms;
}
#app .sort button:hover{
  background: #2a89f8;

}

#app .sort button .selected{
  border-color: #66f897;
}

#app .sort button:not(:first-child){
  margin-left: 10px;
}

.addtask{
  display: var(--header-display);
}

.header{
  height: 80px;
  display: grid; 
  grid-template-columns: 1fr 80px; 
  grid-template-rows: auto; 
  background-color:#66f897;
}

.header .Titel{
  text-align: left;
  margin-left: 20px;
}

.header button{
  font-size: 30px;
  background-color: #57b573;
  border: none;
}
.header button:hover{
  font-size: 40px;
}
</style>
