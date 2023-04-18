<template>
    <div >
        <div v-for="task in tasks" :key="task.id">

            <TaskComponent @toggle-status="$emit('toggle-status',task.id)" @delete-task="$emit('delete-task',task.id)" :task="task" />
        </div>
    </div>
</template>


<script>

import TaskComponent from './Task.vue';


export default {
    
    name: 'TasksComponent',
    props:{
        tasks: Array
    },

    components:{
        TaskComponent
    },
    emits:['delete-task','toggle-status']
}
</script>