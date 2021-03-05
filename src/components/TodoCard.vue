<template>
    <div class="bloc">

        <nav>
            <h2 class="date"> {{ date }} </h2>
            <h1><strong> VueJs Tutorial TodoList</strong></h1>
            <h2 class="task" v-if="tasks.length > 1" > {{tasks.length}} tâches </h2>           <!-- BONUS : Gérer le singulier / pluriel -->
            <h2 class="task" v-else> {{tasks.length}} tâche </h2>
        </nav>

        <div>
            <new-todo @newTask="submitTask" @removeTasks="removeAllTasks"></new-todo>
            <todo-list :tasks="tasks" @doneTask="done" @removeTask="remove" @removeDoneTasks="removeDone"></todo-list>
        </div>

    </div>
</template>


<style>
.bloc{
 
    margin: auto;
    background-color: white;
   
}

nav{
    display: flex;
    justify-content: space-between;
    box-shadow: 0px 3px 4px black;
    padding: 10px 0;
}
.date{
    padding-left: 5%;
}
.task{
     padding-right: 5%;
}
h1{
    color: lightgreen;

}
</style>


<script>
import NewTodo from './NewTodo.vue';
import TodoList from './TodoList.vue';
export default {
    
    name: 'todo-card',
components: {

NewTodo,
TodoList

},
data(){
return {
    tasks: []
}
},
    computed: {
        date: function() {
      let current = new Date();
      let day = current.toLocaleString('default', { weekday: 'long' })
      let month = current.toLocaleString('default', { month: 'long' })
      let date = current.getDate();
      let dateTime = day +' '+ date + ' ' + month ;
      
      return dateTime;
        },

}, 
methods: {

    submitTask(task){
        this.tasks.push({description: task, checked:false})
    },

    done(x){
        if(this.tasks[x].checked === false){
            this.tasks[x].checked = true
        }
        else{
            this.tasks[x].checked = false
        }
    },

    remove(y){
        this.tasks.splice(y, 1)
    },

    removeAllTasks(){
        this.tasks.splice(0)                       //   BONUS : Supprimer toutes les tâches
    },

    removeDone() {
        let index = 0
        this.tasks.forEach(element => {
            if(element.checked === true) {          // BONUS : Supprimer les tâches finies
                element.checked = false
                this.tasks.splice(index, 1)               
            }
            index++
        });
    }
}
}
</script>