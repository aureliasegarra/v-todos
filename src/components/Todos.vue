<template>
    <section class="todoapp">
        <header class="header">
            <h1>Todos</h1>
            <input 
                type="text" 
                class="new-todo" 
                placeholder="Ajouter une tâche" 
                v-model="newTodo"
                @keyup.enter="addTodo"
            >
        </header>
        <div class="main">
            <ul class="todo-list">
                <li 
                    class="todo" 
                    v-for="(todo, index) in todos" 
                    :key="index" 
                    :class="{completed: todo.completed}"
                >
                    <div class="view">
                        <input class="toggle" type="checkbox" v-model="todo.completed">
                        <label>{{ todo.name }}</label>
                    </div>
                </li>
            </ul>
        </div>
    </section>
</template>


<script>
    export default {
       data(){
           return {
               todos: [{
                   name: 'tâche de test',
                   completed: 'false'
               }],
               newTodo: ''
           }
       },
       methods: {
           addTodo () {
               this.todos.push({
                   completed: false,
                   name: this.newTodo
               })
               this.newTodo = ''
           }
       }
    }
</script>



<style src="./todos.css"></style>