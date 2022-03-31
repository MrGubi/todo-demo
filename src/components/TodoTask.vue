<template>
    <div >
        <input v-model="checked" type="checkbox" @click="$emit('toggle-task-event', todoTask.id)"/>
        <p class="title" v-bind:class="{ 'completed' : todoTask.completed }">{{ todoTask.title }}</p>
        <p class="timeleft" :style="timeLeftColor">{{timeLeft}}</p>
        <button @click="$emit('delete-task-event', todoTask.id)">x</button>
    </div> 
</template>

<script>
import prettyMs from 'pretty-ms';

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

    computed: {
        timeLeft() {
            var time = prettyMs(this.todoTask.deadline - new Date().getTime(), {keepDecimalsOnWholeSeconds: true ,compact: true});
            return `${time}`;
        },
        timeLeftColor(){
            var time = prettyMs(this.todoTask.deadline - new Date().getTime(), {keepDecimalsOnWholeSeconds: true ,compact: true});
            var tlColor = "#fff";
            console.log(time.includes('d'));
            console.log(time.includes('h'));
            console.log(time.includes('m','s'));
            if(time.includes('m') || time.includes('s') || time.includes('-')){
                tlColor = "#f52925";
            }
            else if(time.includes('d')){
                tlColor = "#5ab758";
            }
            else if(time.includes('h')){
                tlColor = "#dfab00";
            }
            
            return {'--tl-color': tlColor};
        }
    },
}
</script>

<style scoped>
    .completed {
        text-decoration: line-through;
    }
    div {
        height: 35px;
        display: grid; 
        grid-template-columns: 35px auto 1fr 35px; 
        grid-template-rows: 35px; 
        gap: 0px 0px; 
        grid-template-areas: 
        "Button Title Delete"; 
    }
    button{
        content: "\00d7";
        width: 30px;
        height: 30px;
        text-decoration: none;
        border-radius: 50%;
        border-style: none;
        transition-duration: 100ms;
        padding: 0px;
        color: #fff;
        background-color: #f52925;
        align-self: center;
        font-size: 20px;
        font-style: bold;
        font-weight: 300;
        font-family: Arial, sans-serif;
    }
    
    button:hover{
        font-size: 25px;
    }

    input{
        width: 20px;
        height: 20px;
        align-self: center;
    }
    .title{
        margin: 0px;
        align-self: center;
    }
    .timeleft{
        margin-left: 10px;
        align-self: center;
        justify-self: start;
        width: 50px;
        border: 1px solid #576458;
        border-radius: 5px;
        background: var(--tl-color);
    }
</style>