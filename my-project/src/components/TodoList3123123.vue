<template>
<div>
  <input v-model="newTodo.name" 
  type="text" 
  placeholder="Introduce un nombre"
  :class="{'invalid': !newTodo.invalid}">
  <input v-model="newTodo.email" 
  @keyup.enter="validate"
  type="text" 
  placeholder="Introduce un email"
  :class="{'invalid': !newTodo.invalid}">
  <button type="submit" @click="hideChecks()">hideChecks</button>
  <button type="submit" @click="hideAllChecks()">hideAllChecks</button>
  <button type="submit" @click="completeAll()">completedAll</button>
  <button type="submit" @click="removeAll()">removeAll</button>
  <span v-if="!newTodo.invalid"> wtf is this nigga</span>
  <div v-for="todo in todos" :key="todo.id" :class="{'completed': todo.completed}">
    <div v-if="todo.show">
      <input type="checkbox" v-model="todo.completed" >
      <span>
        {{todo.name}}
      </span>
      <span>
        {{todo.email}}
      </span>
      <button type="submit" @click="removeTodo(todo.email)">remove</button>
      <button type="submit" @click="updateTodo(todo)">updateEmail</button>
    </div>
    <div v-if="todo.update">
        <input v-model="newUpdateTodo.email"
        type="text" 
        placeholder="update todo"
        :class="{'invalid': !todo.invalid}">
    <button type="submit" @click="updateEmail(todo)">updateEmail</button>    
    </div>
  </div>
</div>  
</template>

<script>
const axios = require('axios');

export default {
  data() {
    return {
      newTodo: {
        name: "",
        email: "",
        completed: false,
        invalid: true,
        update: false,
        show: true,
        id: Date.now()
      },
      newUpdateTodo: {
        name: "",
        email: "",
        completed: false,
        invalid: true,
        update: false,
        show: true,
        id: Date.now()
      },
      todos: [
        {}
      ]
    };
  },
  methods: {
    addNewTodo() {
      this.todos.push(this.newTodo);
      this.newTodo = {
        name: "",
        email: "",
        completed: false,
        invalid: true,
        update: false,
        show: true,
        id: 0
      };
    },
    validate() {
      if (!this.todos.some(x => x.email == this.newTodo.email) && this.newTodo.name.length > 6) {
        this.newTodo.invalid = true;
        this.addNewTodo();
      } else {
        this.newTodo.invalid = false;
      }
    },
    removeTodo(email) {
      this.todos = this.todos.filter(todo => todo.email != email);
    },
    updateTodo(todo) {
      todo.update = true;
    },
    updateEmail(lastTodo) {
      lastTodo.email = this.newUpdateTodo.email;
      lastTodo.update = false;
    },
    hideChecks() {
      this.todos.map(todo => {
        if (todo.completed) todo.show = !todo.show;
      });
    },
    hideAllChecks() {
      this.todos.map(todo => {
        todo.show = !todo.show;
      });
    },
    completeAll() {
      this.todos.map(todo => {
        todo.completed = !todo.completed;
      });
    },
    removeAll(){
      this.todos = [];
    }
  }
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
.invalid {
  background-color: #ffdddd;
}
</style>
