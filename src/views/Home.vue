<template>
  <div id="home">
    <AddTodo v-on:add-todo="addTodo" />
    <!--
     First todos is passed as a prop
     the second one is the data we pass
    -->
    <Todos v-bind:todos="todos" v-on:del-todo="deleteToDo" />
  </div>
</template>

<script>
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    async deleteToDo(id) {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);
        this.todos = this.todos.filter(todo => todo.id !== id);
      } catch (err) {
        console.log('🔴', err);
      }
    },
    async addTodo(newTodo) {
      const { title, completed } = newTodo;
      try {
        const res = await axios.post(
          'https://jsonplaceholder.typicode.com/todos',
          {
            title,
            completed
          }
        );
        this.todos = [...this.todos, res.data];
      } catch (err) {
        console.log('🔴', err);
      }
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
