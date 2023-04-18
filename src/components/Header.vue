<template>
    <header>
        <h1>Task Tracker {{title}}</h1>
        <ButtonItem @btn-click="$emit('show-task-form')" :title="showAddTask ? 'Close' : 'Add Task' " color="blue" />
    </header>
</template>

<script>

import ButtonItem from './Button.vue';

export default {
    name: 'HeaderMenu',
    props: {
        title:String,
        showAddTask:Boolean,
        //OR..
        // title:{
        //     type: String,
        //     default: ' Hello world'
        // }
    },
    components:{
        ButtonItem,
    }
}
</script>

<style scoped>

    HeaderMenu{
        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>