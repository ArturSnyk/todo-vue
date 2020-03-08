<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <!--
     First todos is passed as a prop
     the second one is the data we pass
    -->
    <Todos v-bind:todos="todos" v-on:del-todo="deleteToDo" />
  </div>
</template>

<script>
import Todos from './components/Todos';
import Header from './components/layout/Header';
import AddTodo from './components/AddTodo';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Todos,
    Header,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteToDo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
    }
  },
  async created() {
    try {
      const getTodos = await axios.get(
        'https://jsonplaceholder.typicode.com/todos?_limit=5'
      );
      this.todos = getTodos.data;
    } catch (err) {
      console.log('🔴', err);
    }
  }
};
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
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
  background: #667;
}
</style>

// semantics // App is a component // Header is another componant // todos is a
prop we're passing to Todos
