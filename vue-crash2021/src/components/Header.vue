<template>
    <header>
        <h1>{{title}}</h1>
        <Button text="Add Task" color ="green"></Button>
    </header>
</template>

<script>
import Button from './Button'

export default {
    name: 'Header',
    props:{
        title:{
            type: String,//declare prop data type
            default:"Test",//define default value if no props are passed
        }//pass the prop as an object
    },
    components:{
        Button
    }
    
    
}
</script>
<style scoped>
header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>