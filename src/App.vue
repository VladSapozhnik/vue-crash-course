<template>
  <div id="app">
    <h1>todo application</h1>
    <AddTodo
      @add-todo="addTodo"
    />
    <hr>
    <TodoList
      :todos="todos"
      @remove-todo="removeTodo"
    />
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from "@/components/AddTodo";

export default {
  name: 'App',
  components: {
    AddTodo,
    TodoList
  },
  data() {
    return {
      todos: []
    }
  },
  // created: function () {
  //   this.axios.get('https://jsonplaceholder.typicode.com/posts').then(response => {
  //     this.todos = response
  //     this.pending = false
  //   })
  // },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
        .then(response => response.json())
        .then(json => console.log(json))
    this.axios.get('https://jsonplaceholder.typicode.com/todos?_limit=3').then((response) => {
      this.todos = response.data
    })
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
