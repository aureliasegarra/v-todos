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
        <input type="checkbox" class="toggle-all" v-model="allDone">
            <ul class="todo-list">
                <li 
                    class="todo" 
                    v-for="(todo, index) in filteredTodos" 
                    :key="index" 
                    :class="{completed: todo.completed}"
                >
                    <div class="view">
                        <input class="toggle" type="checkbox" v-model="todo.completed">
                        <label>{{ todo.name }}</label>
                        <button class="destroy" @click.prevent="deleteTodo(todo)"></button>
                    </div>
                </li>
            </ul>
        </div>
        <footer class="footer" v-show="todos.length > 0">
            <span class="todo-count"><strong>{{ remaining }}</strong> Tâches à faire</span>
            <ul class="filters">
                <li><a href="#" :class="{selected: filter === 'all'}" @click.prevent="filter = 'all'">Toutes</a></li>
                <li><a href="#" :class="{selected: filter === 'todo'}" @click.prevent="filter = 'todo'">À faire</a></li>
                <li><a href="#" :class="{selected: filter === 'done'}" @click.prevent="filter = 'done'">Faites</a></li>
            </ul>
        </footer>
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
               newTodo: '',
               filter: 'all'
           }
       },
       methods: {
           addTodo () {
               this.todos.push({
                   completed: false,
                   name: this.newTodo
               })
               this.newTodo = ''
           }, 
           deleteTodo (todo) {
               this.todos = this.todos.filter(i => i !== todo)
           }
       },
       computed: {
           allDone: {
               get () {
                   return this.remaining === 0
               },
               set (value) {
                   this.todos.forEach(todo => {
                        todo.completed = value    
                   })
               }
            },
           remaining () {
               return this.todos.filter(todo => !todo.completed).length
           },
           filteredTodos () {
               if (this.filter === 'todo') {
                   return this.todos.filter(todo => !todo.completed)
               } else if (this.filter === 'done') {
                   return this.todos.filter(todo => todo.completed)
               }
               return this.todos
           }
       }
    }
</script>



<style src="./todos.css"></style>