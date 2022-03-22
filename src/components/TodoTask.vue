<template>
    <div>
        {{todoTask.title}}
    </div>    
</template>

<script>
export default {
    name: 'TodoTask',
    props: [
        "todoTask"
    ]
}
</script>