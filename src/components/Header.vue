<template>
    <header>
        <h1>
            {{  title }}
        </h1>
        <ButtonHeader @toggle-add-task="$emit('toggle-add-task')" 
        :text="showAddTask ? 'Close':'Add'" 
        :color="showAddTask ? 'red':'green'"/>
    </header>
</template>

<script>
    import ButtonHeader from './Button'
    export default {
        name: 'HeaderTitle',
        props:{
            title : {
                type : String,
                default: "Hello",
        },
        showAddTask : Boolean
        },
        components:{ 
            ButtonHeader,
        }
    }
</script>

<style scoped> 
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>