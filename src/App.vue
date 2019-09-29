<template>
  <div id="app">
     <Header />
     <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>   
  </div>
</template>

<script>
import Header from './components/layout/Header'
import Todos from './components/Todos'
import AddTodo from './components/AddTodo'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    Header,
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: [ ]
    }
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(err => console.log(err))
    },
    addTodo(newTodo) {
      const {title, compeleted } = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        compeleted
      })
      .then(res =>  this.todos = [...this.todos, res.data] )
      .catch(err => console.log(err));
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=0')
    .then(res => this.todos = res.data)
    .catch(err => console.log(err));
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Poppins&display=swap');
  * {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
  }
  body {
    font-family: 'Poppins', sans-serif;
    width: 60%;
    margin: 0 auto;
    margin-top: 30px;
  }
  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
    font-size: 16px;
  }
  .btn:hover {
    background: #666;
    transition: all 1s;
  }

</style>
