<template>
    <div :key="task.id" v-for="task in tasks">
         <Task 
         @toggle-reminder="$emit('toggle-reminder', task.id)"
         @delete-task="$emit('delete-task', task.id)" 
         :task="task"/>
        
    </div>
    <div v-for="todo in todoList" :key="todo.Id">
        <Task
        @toggle-reminder="$emit('toggle-reminder', todo.id)"
        @delete-task="$emit('delete-task', todo.id)" 
        :task="todo"/>
    </div>
            
     
    
</template>


<script>
import Task from './Task'

import * as axios from 'axios';

export default{
    name: 'Tasks',
    props: {
        tasks: Array,
    },
    components: {
      Task  
    },
    emits:['delete-task', 'toggle-reminder'],
        created(){
            axios
            .get('http://localhost:5001/api/todoitems')
            .then(response => this.todoList=response.data)
        },
        data() {
            return {
                todoList: []
            }
        },
}

</script>