<template>
    <div>
        <h1>My DoTo List</h1>
    </div>
</template>

<script>
export default {
    name: 'TodoContainer',
    data() {
        return {
            tasks: [
                {
                    id: 1,
                    title: "This tasks is IMPORTANT",
                    priority: 5,
                    deadline: '23.03.2022',
                    completed: false,
                },
                {
                    id: 2,
                    title: "This tasks is less important",
                    priority: 3,
                    deadline: '23.03.2023',
                    completed: false,
                },
            ]  
        }
    }
}
</script>