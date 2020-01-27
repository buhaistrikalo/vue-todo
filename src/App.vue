<template>
  <div id="app">
    <h1>Todo</h1>
    <hr>
    <AddTodo 
      @add-todo='addTodo'
    />
    <TodoList 
      v-bind:todos="todos"
      @remove-todo='removeTodo'
    />
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
export default {
  name: 'app',
  data() {
    return {
      todos: [
        {id: 1, title: 'Помыть посуду', completed: false},
        {id: 2, title: 'Помыть пол', completed: false},
        {id: 3, title: 'Постирать билье', completed: false},
        {id: 4, title: 'Поесть', completed: false},
      ]
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json =>{
        this.todos = json
      })
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
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
