<template>
  <div class="home">
    <AddTodo v-on:add-todo="AddTodo"/>
      <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Todos from '@/components/Todos.vue'
import AddTodo from '@/components/AddTodo.vue'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },
  data () {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo (id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      /* eslint-disable no-return-assign */
        .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
        .catch(err => console.log(err))
    },
    AddTodo (newTodo) {
      const { title, completed } = newTodo
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
        /* eslint-disable no-return-assign */
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err))
    }
  },
  created () {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
      /* eslint-disable no-return-assign */
      .then(res => this.todos = res.data)
      .catch(err => console.log(err))
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
