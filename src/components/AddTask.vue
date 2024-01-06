<template>
    <form @submit="onSubmit" class="add-form">
  <label for="task">Task:</label>
  <input type="text" name="Add task" v-model="text" placeholder="Add task"><br><br>

  <label for="dayTime">Day/Time:</label>
  <input type="text" name="dayTime" v-model="dayTime" placeholder="Add Dy & time">

  <label for="reminder">set reminder</label>
  <input type="checkbox" v-model="reminder" name="reminder" >

  <input type="submit" value="SaveTask" class="btn btn-block">
</form>
</template>

<script>
export default {
    name: 'AddTask',
    data() {
        return {
            text: '',
        dayTime: '',
        reminder: false,
        }
        
    },
    methods: {
        onSubmit(e) {
            e.preventDefault()
            if(!this.text) {
                alert('Please add a task')
                return
            }

            const newTask = {
                //id: Math.floor(Math.random() *10000),
                text: this.text,
                day: this.dayTime,
                reminder: this.reminder
            }

            this.$emit('add-task',newTask)

            this.text=''
            this.dayTime=''
            this.reminder=false
        }
    },
    emits: ['delete-task', 'toggle-reminder'],
}
</script>