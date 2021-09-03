<template>
<div class="container">
  <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask"></Header> <!-- when toggle-add-task is fired we excecute toggleAddTask in this component-->
  <div v-show="showAddTask">
      <AddTask @add-task="addTask" />
  </div>
  
  <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks= "tasks"/>
</div>

</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'
//import Button from './components/Button'
export default {
  name: 'App',
  components: {
    Header, //Register Component
    Tasks,
    AddTask
  },
  data(){
    return{
      tasks:[],
      showAddTask: false
    }
  },
  methods:{
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    },
    async addTask(task){
        const res = await fetch('http://localhost:5000/tasks', {
        method: 'POST',
        headers:{
          'Content-type': 'application/json',
          body: JSON.stringify(task)
        }
      })
      const data = await res.json()

      this.tasks = [...this.tasks, data] //spread accross array and add new task 
    },
    deleteTask(id){
      
      if (confirm('Are you sure?')){
        this.tasks = this.tasks.filter((task)=>task.id != id)
      }
      
    },
    toggleReminder(id){
      this.tasks = this.tasks.map((task)=> //map to manipulate the array and return a new array of updated tasks
       task.id === id ? {...task,reminder: !task.reminder} : task) //if task.id is equal to id param  return array of intial task properties change reminder to opposite, else return task

    },
    async fetchTasks(){
      const res = await fetch('http://localhost:5000/tasks') //returns promise so we need to await

      const data = await res.json()

      return data
    },
    async fetchTask(id){
      const res = await fetch(`http://localhost:5000/tasks/${id}`) //returns promise so we need to await

      const data = await res.json()

      return data
    },



  },
  
  async created(){
    this.tasks = await this.fetchTasks()
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body{
  font-family: 'Poppins',sans-serif;
}
.container{
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;

}

.btn{
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
}
</style>
