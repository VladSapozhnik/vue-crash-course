<template>
  <div>
    <h2>todo application</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <AddTodo
        @add-todo="addTodo"
    />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>
    </select>
    <Loader v-if="loading"/>
    <TodoList
        v-else-if="filteredTodos.length"
        :todos="filteredTodos"
        @remove-todo="removeTodo"
    />
    <p v-else>No Todos!</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from "@/components/AddTodo";
import Loader from "@/components/Loader";

export default {
  name: 'App',
  components: {
    AddTodo,
    TodoList,
    Loader
  },
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  // created: function () {
  //   this.axios.get('https://jsonplaceholder.typicode.com/posts').then(response => {
  //     this.todos = response
  //     this.pending = false
  //   })
  // },
  // watch: {
  //   filter(value) {
  //     console.log(value)
  //   }
  // },

  //функции в computed являются переменными
  computed: {
    filteredTodos() {
      if (this.filter === 'completed') {
        return this.todos.filter(t => t.completed)
      } else if (this.filter === 'not-completed') {
        return this.todos.filter(t => !t.completed)
      }
      return this.todos
    }
  },
  mounted() {
    // fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
    //     .then(response => response.json())
    //     .then(json => console.log(json))
    this.axios.get('https://jsonplaceholder.typicode.com/todos?_limit=3').then((response) => {
      setTimeout(() => {
        this.todos = response.data
        this.loading = false
      }, 1000)
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