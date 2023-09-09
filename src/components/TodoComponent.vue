<template>
    <div class="container">
        <div class="row">
            <h2>todo list</h2>
            <ul class="list-group">
                <li class="list-group-item list-group-item-action active">
                    <strong class="">Your Tasks</strong> 
                    <span class="float-end" @click="wantAdd"><i :class="afficherChampNouveau ? 'fa-solid text-danger fa-circle-minus': 'fa-solid fa-square-plus fa-lg'" id="boutonAddOrReset"></i></span>
                    <input v-show="afficherChampNouveau" type="text" class="form-control" name="" id="wantAddId" @keyup.enter="addNewTodo" v-model="todo.name">
                </li>
                <li v-for="todo in todos" :key="todo.name" class="list-group-item" :class="{achieve: todo.done}">
                    <input v-model="todo.done" class="form-check-input me-1 mb-1 float-start" type="checkbox" value="" aria-label="...">
                    <span class="float-start">{{ todo.name }}</span>
                    <span class="float-end"><i class="fa-solid text-danger fa-circle-minus"></i></span>
                    <input type="text" class="form-control" name="" id="">
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


//const testTodo = new Todo("Tache de test", false);
export default {
    data() {
        return {
            todo: {
                name: "",
                done: false,
            },
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
        addNewTodo() {
            this.todos.push({
                name: this.todo.name,
                done: this.done,
            })
            this.todo.name = ""
            this.afficherChampNouveau = false;
        },
    },
    created() {
        //this.todos.push(testTodo)
    }
}

</script>

<style scoped>
    .achieve{
        background-color: rgba(0, 0, 0, .07);
    }
</style>