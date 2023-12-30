<template>
    <div  :key="task.id" v-for="task in tasks">
        <TaskObject :task="task" />
    </div>
    
</template>

<script>
    import TaskObject from './Task'
    export default {
        name:'TasksHeader',
        props: {
            tasks: Array
        },
        components:{
            TaskObject
        }
    }
</script>