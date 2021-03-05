<template>
    <ul>
        <li v-for="(task, index) in tasks" :key="(task, index)">
            <input type="checkbox" v-on:click='done(index)'>
            <p v-bind:class="{'done':task.checked}">{{task.description}}</p>
            <button v-on:click='remover(index)' class="delete is-large"></button>
        </li>
        <li>
            <button v-on:click="removeDoneTasks">Supprimer toutes les tâches finies</button>
        </li>
    </ul>
</template>


<style scoped>
li {
    display: flex;
    justify-content: space-around;
    margin: 2%;
}

.done{
    text-decoration: line-through;
    font-style: italic;
    color: red;
}
</style>


<script>
export default {
    name: 'todo-list',
    props: ['tasks'],
    methods: {
        done(index){
            this.$emit('doneTask', index)
        },

        remover(index){
            this.$emit('removeTask' , index)
        },

        removeDoneTasks(){
            this.$emit('removeDoneTasks')
        }
    }
}
</script>