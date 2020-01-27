<template>
  <div id="app">
    <router-link to='/'>Home</router-link>
    <AddTodo 
      @add-todo='addTodo'
    />
    <select v-model="filter">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="not-completed">Not Completed</option>
    </select>

    <Loader v-if='loading' />
    <TodoList 
        v-else-if='filteredTodos.length'
        v-bind:todos="filteredTodos"
        @remove-todo='removeTodo'
    />
    <p v-else>No todos</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'
export default {
  name: 'app',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json =>{
        this.todos = json
        this.loading = false
      })
  },
  computed: {
    filteredTodos() {
        if (this.filter === 'all') {
            return this.todos
        } 
        else if (this.filter === 'completed') {
            return this.todos.filter(t => t.completed)
        }
        else {
            return this.todos.filter(t => !t.completed)
        }
    }      
  },
  methods: {
    removeTodo(id){
      this.todos= this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    },
  },
  components: {
    TodoList,
    AddTodo,
    Loader,
  }
}
</script>