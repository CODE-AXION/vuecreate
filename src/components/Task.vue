<template>
    <div>
       <div @dblclick="$emit('toggle-status',task.id)" :class="[task.status ? 'text-green-700' : '', 'flex items-center justify-center gap-4 mt-2 bg-slate-200 rounded w-1/2 p-4 mx-auto' ]" >
            <h3> {{task.id}} </h3>
            <div>{{task.text}}</div>
            <p>{{task.status}}</p>
            <div @click="$emit('delete-task',task.id)" class="text-red-700 p-2 bg-red-200 rounded">X</div>
        </div>
        
    </div>
</template>

<script>

export default {
    name: 'TaskComponent',
    props:{
        task: Object
    },



}

</script>
