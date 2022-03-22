<template>
    <div v-bind:class="{'completed' : todoTask.completed}">
        <p @click="toggleComplete">{{todoTask.title}}</p>
    </div>    
</template>

<script>
export default {
    name: 'TodoTask',
    methods: {
        toggleComplete() {
            this.todoTask.completed = !this.todoTask.completed
        }
    },
    props: [
        "todoTask"
    ]
}
</script>

<style>
    .completed {
        text-decoration: line-through;
    }
</style>