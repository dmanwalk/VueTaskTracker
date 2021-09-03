<template>
    <header>
        <h1>{{title}}</h1>
        <Button @btn-click="$emit('toggle-add-task')" :text="showAddTask ? 'Close':'Add Task'" :color ="showAddTask ? 'red' : 'green'"></Button>
    </header>
</template>

<script>
import Button from './Button'

export default {
    name: 'Header',
    props:{
        title: String,
        showAddTask: Boolean,//declare prop data type
            //define default value if no props are passed
        //pass the prop as an object
        
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