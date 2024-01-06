<template>
    <div  :key="task.id" v-for="task in tasks">
        <TaskObject @toggle-reminder="$emit('toggle-reminder', task.id)" @delete-task="$emit('delete-task', task.id)" :task="task" />
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
        },
        emits: ['delete-task', 'toggle-reminder'],
    }
</script>