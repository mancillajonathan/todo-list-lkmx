<template>
  <div id="app">
    <h1>TODO list</h1>

    <form @submit.prevent="addTodo">
      <input type="text" v-model="newTodo">
      <button :disabled="!newTodo">Add</button>
    </form>

    <ul>
      <li v-for="(todo, index) in todos" :key="index">

        <div v-show="!isUpdateFormVisible[index]">
          {{ todo }}

          <span @click="showUpdateForm(index)">Editar</span>&nbsp;
          <span @click="removeTodo(index)">Eliminar</span>
        </div>

        <form @submit.prevent="updateTodo(index)"
          v-show="isUpdateFormVisible[index]">

          <input type="text" v-model="updatableTodo">
          <button>Editar</button>
        </form>
      </li>
    </ul>

  </div>
</template>

<script>
export default {
  data() {
    return {
      // list of todos
      todos: [],

      // new todo
      newTodo: '',

      // selected todo to update
      updatableTodo: '',

      // keeps track of whether the update form is visible or no
      // for each todo
      isUpdateFormVisible: {},
    }
  },
  methods: {
    addTodo() {
      this.todos.push(this.newTodo);
      this.newTodo = '';
    },

    removeTodo(index) {
      this.todos.splice(index, 1);
    },

    updateTodo(index) {
      this.$set(this.todos, index, this.updatableTodo);
      this.$set(this.isUpdateFormVisible, index, false);
    },

    showUpdateForm(index) {
      this.updatableTodo = this.todos[index];

      // close all forms first
      for (let i = 0; i < this.todos.length; i++) {
        this.$set(this.isUpdateFormVisible, i, false);
      }

      this.$set(this.isUpdateFormVisible, index, true);
    }
  }
}
</script>
