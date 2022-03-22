<template>
    <div>
        <form @submit="addTask">
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

export default {
    name: 'AddTask',
    data() {
        return {
            title: '',
            priority: '1',
        }
    },
    methods: {
        addTask(event){
            event.preventDefault();

            const newTask = {
                id: uuidv4(),
                title: this.title,
                priority: this.priority,
                deadline: '23.03.2022',
                completed: false
            }

            this.$emit("add-task-event", newTask)
            this.title = '';
        }
    }
}
</script>