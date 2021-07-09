<template>
    <div class="task-card" v-bind:class="task.status">
        
        <div v-if="!toggle" v-on:dblclick="toggleEdit(true)">
            <input class="toggledTask" v-model=task.task v-on:keyup.enter="toggleEdit(true), $parent.editTask(task.task_id, task.task)">
            <button class="delete" v-on:click="$parent.deleteTask(task.task_id)">
                <icon name="times"></icon>
            </button> 

            <button class="edit" v-on:click="toggleEdit(true)">
                <icon name="pencil-alt"></icon>
            </button>  

            <button class="complete" v-on:click="completeTask(task.task_id)">
                <icon name="check"></icon>
            </button> 
        </div>

        <div v-else v-on:dblclick="toggleEdit(false)">
            {{task.task}}
            <button class="delete" v-on:click="$parent.deleteTask(task.task_id)">
                <icon name="times"></icon>
            </button> 

            <button class="edit" v-on:click="toggleEdit(false)">
                <icon name="pencil-alt"></icon>
            </button>  

            <button class="complete" v-on:click="completeTask(task.task_id)">
                <icon name="check"></icon>
            </button> 
        </div>

    </div>
</template>


<script>

import axios from 'axios';

export default {
    name: 'Task',
    props:{
        task: {
            type: Object
        }
    },
    data(){
        return{
            toggle: true,
            message: ""
        }
    },
    methods: {
        completeTask: function(id){
            axios.put("/task/status", {
                task_id: id, status: "complete"
            }).then(() => {
                this.task.status = "complete"
            }).catch()
        },
        toggleEdit: function(toggle){
            this.toggle = toggle
        }
    }
}

</script>


<style scoped>

.pending{
  color:grey;
  font-weight: bold;
}

.complete{
  color:green;
  text-decoration: line-through;
}

.task-card{
    border-bottom: lightgray;
    border-bottom-width: 0.1em; 
    border-bottom-style: solid; 
    margin: 1em auto;
    padding: 0.4em;
    border-radius: 0.5em; 
}

.task-card button.delete{
    color: grey;
    float: right;
    margin: 0.12em;
    border-radius: 0.5em;
    background: whitesmoke;
    border: none;
    outline: none;
}

.task-card button.complete{
    color: green;
    float: right;
    margin: 0.12em;
    border-radius: 0.5em;
    background: whitesmoke;
    border: none;
    outline: none;
}

.task-card button.edit{
    color: black;
    float: right;
    margin: 0.12em;
    border-radius: 0.5em;
    background: whitesmoke;
    border: none;
    outline: none;
}

.task-card input.toggledTask{
    background: whitesmoke;
    border: solid;
    border-color: lightblue;
    border-radius: 0.5em; 
    outline: none;
    font-weight: inherit;
    font-size: inherit;
    color: gray;
    width: 50%; 
    height: 1em;
    box-shadow: 0 0 1em lightblue;
}

</style>