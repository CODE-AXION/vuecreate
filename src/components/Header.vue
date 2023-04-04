<template>
    <header>
        <h1>Tast Tracker {{title}}</h1>
    </header>
</template>

<script>

export default {
    name: 'HeaderMenu',
    props: {
        title:{
            type: String,
            default: ' Hello world'
        }
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