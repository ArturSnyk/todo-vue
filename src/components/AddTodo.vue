<template>
  <div>
    <form @submit="addTodo">
      <input type="text" name="title" v-model="title" placeholder="Add Todo ..." />
      <input type="submit" class="btn" />
    </form>
  </div>
</template>

<script>
import { uuid } from 'uuidv4';
export default {
  name: 'AddTodo',
  data() {
    return {
      title: ''
    };
  },
  methods: {
    addTodo(e) {
      if (this.title) {
        // we don't want to form to acctualy submit to a file
        e.preventDefault();
        const newTodo = {
          id: uuid(),
          title: this.title,
          completed: false
        };
        // sending uo the new todo to parent
        this.$emit('add-todo', newTodo);
        // after submiting the form will clear
        this.title = '';
      }
    }
  }
};
</script>

<style>
form {
  display: flex;
}
input[type='text'] {
  flex: 10;
  padding: 5px;
}
input[type='submit'] {
  flex: 2;
}
</style>
