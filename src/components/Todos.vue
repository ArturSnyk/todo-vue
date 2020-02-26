/* eslint-disable vue/valid-template-root */
<template>
  <div>
    <div v-bind:key="todo.id" v-for="todo in todos">
      <h2>{{todo.title}}</h2>
    </div>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: ["todos"]
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
