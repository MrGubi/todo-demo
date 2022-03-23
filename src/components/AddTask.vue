<template>
    <div>
        <form @submit="addTask">
            <datepicker v-model="date"/>
            <input type="text" v-model="title" name="title"/>
            <select v-model="priority">
                <option value="1">1</option> 
                <option value="2">2</option> 
                <option value="3">3</option>
                <option value="4">4</option> 
                <option value="5">5</option>
            </select>
            <button type="submit">Hinzufügen</button>
        </form>
    </div>
</template>

<script>
import {v4 as uuidv4} from 'uuid';
import Datepicker from 'vue3-date-time-picker';
import 'vue3-date-time-picker/dist/main.css';
import { ref } from "vue";

export default {
    name: 'AddTask',
    components: {
        Datepicker
    },
    data() {
        return {
            title: '',
            priority: '1',
        }
    },
    setup() {
    const date = ref(new Date());

    return {
      date,
    };
  },
    methods: {
        addTask(event){
            event.preventDefault();

            const newTask = {
                id: uuidv4(),
                title: this.title,
                priority: this.priority,
                deadline: this.date,
                completed: false
            }

            this.$emit("add-task-event", newTask)
            this.title = '';
        }
    }
}
</script>