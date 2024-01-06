<template>
  <div class="container">
    <HeaderTitle @toggle-add-task="onToggleAddTask" title="Task Tracker" :showAddTask="showAddTask"/>
    <div v-if="showAddTask">
      <AddTask @add-task="addTask"/>
    </div>
    
    <TasksHeader @toggle-reminder="onToggleReminder" @delete-task="onDeleteTask" :tasks="tasks"/>
  </div>
</template>

<script>
import HeaderTitle from './components/Header'
import TasksHeader from './components/Tasks'
import AddTask from './components/AddTask'

export default {
  name: 'App',
  components: {
    HeaderTitle,
    TasksHeader,
    AddTask,
  },
  data() {
    return {
      tasks:[],
      showAddTask: false
  }
},
methods:{
  async onDeleteTask(id){
    if(confirm('sure to delete')) {
      

      const res=await fetch(`api/tasks/${id}`, {
      method: 'DELETE',
      headers:{
        'Content-type':'application/json',
      },
    })
    res.status === 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id)) : alert('Erorr deleting task')
    }
    
  },
  async onToggleReminder(id) {
    console.log(id)

    const taskToToggle = await this.fetchTask(id);
    console.log(taskToToggle)
    const updateTask = {...taskToToggle, reminder: !taskToToggle.reminder}
    console.log("update task is ", taskToToggle)

    const res=await fetch(`api/tasks/${id}`, {
      method: 'PUT',
      headers:{
        'Content-type':'application/json',
      },
      body: JSON.stringify(updateTask)
       })
       const data = await res.json();
       console.log(data)
       this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: data.reminder} : task);
   
  },
  onToggleAddTask(){
    this.showAddTask=!this.showAddTask
  },
  async addTask(newTask) {
    console.log('reached app')

    const res=await fetch('api/tasks', {
      method: 'POST',
      headers:{
        'Content-type':'application/json',
        
      },
      body: JSON.stringify(newTask)
    })
    const data = await res.json()
    this.tasks = [...this.tasks, data]
},
async fetchTasks() {
  const res = await fetch('api/tasks')

  const data = await res.json();

  return data;
},
async fetchTask(id) {
  const res = await fetch(`api/tasks/${id}`, {
      method: 'GET',
      headers:{
        'Content-type':'application/json',
      },
    })

  const data = await res.json();

  return data;
}
},

  async created() {
    this.tasks = await this.fetchTasks()
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
