<template>
    <div v-bind:class="{ 'completed' : todoTask.completed }">
        <p>{{ todoTask.title }} - {{todoTask.deadline}} - {{todoTask.priority}}</p>
        <input v-model="checked" type="checkbox" @click="$emit('toggle-task-event', todoTask.id)"/>
        <button @click="$emit('delete-task-event', todoTask.id)">Löschen</button>
    </div> 
</template>

<script>
export default {
    name: 'TodoTask',
        props: [
        "todoTask"
    ],
    data() {
        return {
            checked: this.todoTask.completed,
            localTask: this.todoTask
        }
    },
    methods: {

    },
    watch: {
        
    }
}
</script>

<style>
    .completed {
        text-decoration: line-through;
    }
</style>