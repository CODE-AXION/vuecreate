<template>
  <div>
    <HeaderMenu @show-task-form="toggleForm" title="Hello world" :showAddTask="showAddTask" />

    <div v-show="showAddTask">
      <AddTaskComponent @add-event="addTask" />
    </div>
    <TasksComponent @toggle-status="toggleStatus" @delete-task="deleteTask" :tasks="tasks" />
  
    <router-view></router-view>
    <FooterComponent />
  </div>
</template>

<script>

import HeaderMenu from './components/Header.vue';
import TasksComponent from './components/Tasks.vue';
import AddTaskComponent from './components/AddTask.vue';
import FooterComponent from './components/Footer.vue';

import axios from 'axios';

export default {
  
  name: 'App',

  components: {
    HeaderMenu,
    TasksComponent,
    AddTaskComponent,
    FooterComponent
  },

  data(){
    return {
      
      tasks:[],

      showAddTask: false
    }
  },
  methods:{

    toggleForm(){
      this.showAddTask = !this.showAddTask
    },

    async addTask(task){

      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task),
      })
      const data = await res.json()

      // const response = await axios({
      //   method: 'post',
      //   url: '/api/tasks',
      //   responseType: 'json',
      //   headers: {
      //     'Content-Type': 'application/json'
      //   },
      //   data: {
      //     task: task
      //   }
      // });

      this.tasks = [...this.tasks, data]
    },

    async deleteTask(id){
      
     if (confirm('Are you sure?')) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE',
        })
        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert('Error deleting task')
      }
    },

    async toggleStatus(id){

      const taskToToggle = await this.fetchServerSingleTask(id)
      
      const updTask = { ...taskToToggle, status: !taskToToggle.status }

      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updTask),
      })
      const data = await res.json()

      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, status: data.status } : task
      )
    },

    async fetchServerTasks(){
      
      const response = await axios.get('api/tasks');
      // handle success
      return response.data;
    },

    async fetchServerSingleTask(id){
      
      const response = await axios.get(`api/tasks/${id}`);
      // handle success
      return response.data;
    }

  }
  ,
  async created(){
    this.tasks = await this.fetchServerTasks()
  }
}
</script>

<style>

#app {

  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
