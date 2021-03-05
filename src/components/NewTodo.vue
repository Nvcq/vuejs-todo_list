<template>
    <div class="form">
        <input v-model="task" class="input is-primary" type="text" placeholder="Nouvelle tâche...">
        <button v-on:click='addTask' class="button is-success">+</button>
        <button v-on:click='removeAllTasks' class="delete is-large"></button>
    </div>
</template>
<style scoped>
input{
    width: 30%;
margin: 5% 0px;
border-left: none;
border-top: none;
border-right: none;
border-bottom: 4px solid lightgreen;
}
button{
margin: 5% 10px;
border-radius: 100px;
font-weight: bold;
}

</style>

<script>
export default {
    name: 'new-todo',
    data(){
        return {
            task: '',
            }
    },
    methods: {
        addTask(){
            this.$emit('newTask', this.task)
        },

        removeAllTasks(){
            this.$emit('removeTasks')
        }
    }
}
</script>
