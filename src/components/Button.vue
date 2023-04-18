<template>
    <button @click="onClick()" :style="{color:color}">
        {{title}}
    </button>
</template>

<script>

export default {
    name:'ButtonItem',
    props:{
        title: String,
        color: String,
    },
    methods:{
        onClick(){
           this.$emit('btn-click')
        }
    }  
}

</script>