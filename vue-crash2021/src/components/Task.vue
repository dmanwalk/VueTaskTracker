<template>
<div @dblclick="$emit('toggle-reminder',task.id)"  :class="[task.reminder ? 'reminder' : '', 'task']">  <!-- If task. reminder is true, add the reminder class, else add no class to div and always apply the task class-->
<h3>
    {{task.text}}
    <i @click="onDelete(task.id)" class="fas fa-times"></i>
</h3>
<p>{{task.day}}</p>
</div>
    
</template>

<script>
export default {
    name: 'Task',
    props:{
        task: Object,
    },
    methods:{
        onDelete(id){
            this.$emit('delete-task', id) ///emitting a custom callback function delete-task and passing the id as a param up to tasks
        },
    }
}

</script>

<style scoped>
.fas{
    color: red;
}
.task{
    background: #f3f3f3;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
}
.task h3{
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.task.reminder{
    border-left: 5px solid green;
}
</style>