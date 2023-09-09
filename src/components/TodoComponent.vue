<template>
    <div class="container">
        <div class="row">
            <h2>todo list</h2>
            <ul class="list-group">
                <li class="list-group-item list-group-item-action active">
                    <input type="checkbox" class="float-start form-check-input me-1 mb-1" v-model="allTodosIsDone">

                    <strong class="">Your Tasks</strong> 
                    <span class="float-end" @click="wantAdd"><i :class="afficherChampNouveau ? 'fa-solid text-danger fa-circle-minus': 'fa-solid fa-square-plus fa-lg'" id="boutonAddOrReset"></i></span>
                    <input v-show="afficherChampNouveau" type="text" class="form-control" name="" id="wantAddId" @keyup.enter="addNewTodo" v-model="todo_.name">
                </li>
                <li v-for="todo in todos" :key="todo.name" class="list-group-item" :class="{achieve: todo.done}">
                    <input v-model="todo.done" v-if="!todo.estEnModification" class="form-check-input me-1 mb-1 float-start" type="checkbox" value="" aria-label="...">
                    <span v-if="!todo.estEnModification" class="float-start" @dblclick="wantUpdate(todo)">{{ todo.name }}</span>
                    <span class="float-end" @click="deleteTodo(todo)"><i class="fa-solid text-danger fa-circle-minus"></i></span>
                    <input type="text" :value="todo.name" @keyup.enter="changeTodoName(todo)" v-if="todo.estEnModification" class="form-control" name="" id="champModif">
                </li>
            </ul>
        </div>
    </div>
</template>
<style scoped>
h2{
    text-transform: capitalize;
}
</style>
<script>
import { nextTick } from 'vue';


const testTodo = {name: "Tache de test", done: false, estEnModification: false};
export default {
    data() {
        return {
            todo_: {
                name: "",
                done: false,
                estEnModification: false,
            },
            // allTodosIsDone: false,
            todos: [],
            afficherChampNouveau: false,
        }
    },
    methods: {
        wantAdd() {
            this.afficherChampNouveau = !this.afficherChampNouveau;
            nextTick(function() {
                document.getElementById('wantAddId').focus();
            })
            
        },
        wantUpdate(todo){
            todo.estEnModification = true;
            nextTick(() => {
                document.getElementById('champModif').focus();
            });
            
        },
        changeTodoName(todo){
            
            if(event.target.value != "") {
                todo.name = event.target.value; 
                todo.estEnModification = false;
            }else{
                alert('Inséré une valeur comme nom de votre tâche')
            }

        },
        addNewTodo() {
            this.todos.push({
                name: this.todo_.name,
                done: false,
            })
            this.todo_.name = ""
            this.afficherChampNouveau = false;
        },
        deleteTodo(thisTodo){
            this.todos = this.todos.filter(function(todo){
                return todo != thisTodo
            })
        },
        
    },
    // watch: {
    //     allTodosIsDone() {
    //         if(this.allTodosIsDone){
    //             this.todos.forEach(todo => {
    //                 todo.done = true;
    //             });
    //         }else{
    //             this.todos.forEach(todo => {
    //                 todo.done = false;
    //             });
    //         }
    //         this.todos.every((todo) => todo.done === true)
    //     },
    // },
    computed: {
        allTodosIsDone:{
            get () {
               return this.todos.filter((todo) => todo.done==false).length == 0
            },
            set(value){
                for(let i = 0; i<this.todos.length; i++){
                    this.todos[i].done = value;
                }
            }
        }
    },
    created() {
        this.todos.push(testTodo)
    }
}


</script>

<style scoped>
    .achieve{
        background-color: rgba(0, 0, 0, .07);
    }
</style>