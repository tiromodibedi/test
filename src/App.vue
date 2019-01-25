<template>
  <div id="app">
    <Header/>
    <AddTodo v-on:add-todo="addTodo" />
    <!-- pass the array into the todos component -->
    <Todos v-bind:todos="todos" v-on:del-todo-up="deleteTodo" />
  </div>
</template>

<script>
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';
import Header from './components/layout/Header';

import axios from 'axios';

export default {
  name: 'app',
  components: {
    AddTodo,
    Header,
    Todos
  },
  data() {
    return {
      todos: []
    }
  },
  // methods in the component
  methods: {
    deleteTodo(id) {
      // console.log(id);
      this.todos = this.todos.filter((todo) => {
        return todo.id !== id;
      });
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        /* eslint-disable */
        .catch((err) => console.log(err));
    }
  },
  // when the component is initialised
  created() {
    // initialise
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(res => {
        this.todos = res.data
      })
      /* eslint-disable */
      .catch(err => console.log(err));
  }
  
}
</script>

<style>
/* Global Styles */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
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
