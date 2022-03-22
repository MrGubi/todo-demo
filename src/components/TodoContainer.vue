<template>
    <div>
        <h1>My DoTo List</h1>
        <ul class="wrapper">
            <li v-bind:key="task.id" v-for="task in tasks" class="item">
                <todoTask v-bind:todoTask="task"/>
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