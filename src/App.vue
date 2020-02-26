<template>
  <div id="app">
    <HelloWorld msg="Hello World!" />
    <!--
     First todos is passed as a prop
     the second one is the data we pass
    -->
    <Todos v-bind:todos="todos" />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld";
import Todos from "./components/Todos";

export default {
  name: "App",
  components: {
    HelloWorld,
    Todos
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "Todo one",
          compleate: false
        },
        {
          id: 2,
          title: "Todo two",
          compleate: true
        },
        {
          id: 3,
          title: "Todo three",
          compleate: false
        }
      ]
    };
  }
};
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

// semantics // App is a component // HelloWorld is another componant // msg is
a prop we're passing to HelloWord
