<template>
  <div>
      <input v-model="newTodo.text" 
  @keyup.enter="addTodo"
  type="text" 
  placeholder="Introduce un email">
  <div v-for="todo in todos" :key="todo.id">
      <span>{{todo.text}}</span>
      <button @click="removeTodo(todo)" >remove</button>
      <input v-model="newUpdateTodo.text" 
  type="text" 
  placeholder="update Todo">
      <button type="submit" @click="updateTodo(todo)" >update</button>
  </div>
  </div>
</template>

<script>
const axios = require("axios");

export default {
  data() {
    return {
      newTodo: {
        text: "",
        isCompleted: false,
        createdAt: Date.now()
      },
      newUpdateTodo: {
        text: "",
        isCompleted: false,
        createdAt: Date.now()
      },
      todos: []
    };
  },
  created() {
    axios
      .get("http://localhost:2222/api/TODOS")
      .then(response => (this.todos = response.data))
      .catch(error => console.log(error));
  },
  methods: {
    addTodo() {
      axios
        .post("http://localhost:2222/api/TODOS", this.newTodo)
        .then(response => {
          this.todos.push(response.data);
          this.newTodo = {
            text: "",
            isCompleted: false,
            createdAt: Date.now()
          };
        })
        .catch(error => console.log(error));
    },
    removeTodo(todo) {
      axios
        .delete(`http://localhost:2222/api/TODOS/${todo._id}`)
        .then(response => {
          this.todos = this.todos.filter(x => x._id != todo._id);
        })
        .catch(error => console.log(error));
    },
    updateTodo(todo) {
      axios.patch(
          `http://localhost:2222/api/TODOS/${todo._id}`,
          this.newUpdateTodo
        )
        .then(response => {
          this.todos.forEach(x => {
            if (x._id == todo._id) {
              x.text = response.data.text;
            }
          });
          this.newUpdateTodo = {
            text: "",
            isCompleted: false,
            createdAt: Date.now()
          };
        })
        .catch(error => console.log(error));
    }
  }
};
</script>

<style>

</style>


