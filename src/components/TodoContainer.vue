<template>
    <div>
        <ul class="wrapper">
            <li v-bind:key="task.id" v-for="task in tasks" class="item">
                <todoTask v-bind:todoTask="task" @toggle-task-event="$emit('toggle-task-event', task.id)" @delete-task-event="$emit('delete-task-event', task.id) "/>
            </li>
        </ul>
    </div>
</template>

<script>
import TodoTask from './TodoTask.vue'

export default {
    name: 'TodoContainer',
    components: {
        TodoTask
    },
    props: [
        "tasks"
    ]
}
</script>

<style scoped>
    li{
        background-color: #d9dddd;
        margin-top: 3px;
        margin-bottom: 3px;
        border-left: solid #b7bbbb;
    }
    ul{
        margin-top: 10px;
        margin-bottom: 10px;
        padding: 2px;
        list-style-type: none;
    }
</style>