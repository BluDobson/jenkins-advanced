<template>
    <div class="tasklist">

      <NewTask/>

    <div v-for="task in tasks" v-bind:key="task.task_id">
      <Task v-bind:task="task"/>       
    </div>

    </div>
</template>


<script>

import Task from './Task.vue';
import NewTask from './NewTask.vue';
import axios from 'axios';

export default {
    name: "Tasklist",
    components: {
      Task, 
      NewTask
    },
    data(){
      return {
        tasks: []
      }
    },
    created: function(){
      this.getTasks();
    },
    methods: {
      getTasks: function(){
        axios.get("/task/gettasks").then((response)=>{
          this.tasks = response.data;       
        }).catch()
      },
      deleteTask: function(id){
        axios.delete("/task/deleteone", {
          data: {task_id: id}
        }).then(() => {
          this.tasks.forEach((task, index) => {
            if(task.task_id === id){
              this.tasks.splice(index, 1)
            }
          })
        }).catch()
      },
      insertTask: function(input){
        if (input !== ""){
          axios.post("/task/insertone", {
            task: input
          }).then(() => {
            this.getTasks()
          }).catch()
        }
      },
      editTask: function(id, editedTask){
        axios.put("/task/edittask", {
            task_id: id, task: editedTask
        }).then(() => {
          this.getTasks()
        }).catch()
      }   
    }
}

</script>


<style scoped>

.tasklist{
    margin: 0 13em;
    padding: 0em;
    background: whitesmoke;
    border-bottom-left-radius: 1em; 
    border-bottom-right-radius: 1em;
}

</style>