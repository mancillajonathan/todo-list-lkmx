<template>
  <div id="app">
    <h1>ToDo List</h1>

    <form @submit.prevent="addTodo" id="formTodo">
      <input type="text" v-model="newTodo" id="todoInput" placeholder="Today's goal is...">
      <button :disabled="!newTodo" id="add">Add new task</button>
    </form>

    <ul>
      <li v-for="(todo, index) in todos" :key="index">

        <div v-show="!isUpdateFormVisible[index]" id="divList">
          <span id="activity">{{ todo }}</span>
          <span @click="showUpdateForm(index)" class="btn" id="btnEdit">Edit</span>&nbsp;
          <span @click="removeTodo(index)" class="btn" id="btnDelete">Delete</span>
        </div>

        <form @submit.prevent="updateTodo(index)"
          v-show="isUpdateFormVisible[index]">

          <input type="text" v-model="updatableTodo" id="inputSave">
          <button class="btn" id="btnSave">Save</button>
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


<style>
* {
  font-family: 'roboto';
}
body {
  background-color: #E8E8E8;
  display: flex;
  align-content: center;
  justify-content: center;
}

h1 {
  font-weight: bold;
  margin-bottom: 28px;
}

#formTodo {
  display: flex;
  justify-content: space-between;
  background-color: #ffffff;
  padding: 18px;
  box-shadow: 0px 16px 40px rgba(228, 214, 215, 0.2);
  border-radius: 4px;
}

#todoInput {
  width: 400px;
  height: 48px;
  box-sizing: border-box;
  background-color: #EAEAEA;
  border-style: none;
  margin-right: 18px;
  border-radius: 4px;
  padding: 6px 16px 6px  16px;
  font-size: 24px;
}

#add {
  height: 48px;
  font-size: 24px;
  background-color: #3959A2;
  padding: 6px 30px 6px 30px;
  border-style: none;
  color: #ffff;
  border-radius: 4px;
  font-weight: bold;
}

ul {
  background-color: #ffffff;
  margin: 0;
  padding-bottom: 22px;
}

#divList {
  display: flex;
  align-items: center;
  padding-right: 18px;
  margin-bottom: 14px;
}

#activity {
  width: 100%;
  display:inline-block;
  height: 28px;
  font-size: 24px;
}

.btn {
  display:inline-block;
  border: 2px solid #C4C4C4;
  height: 48px;
  padding: 10px 22px;
  box-sizing: border-box;
  font-weight: 500;
  font-size: 24px;
  color: #838383;
  margin-left: 18px;
}

.btn:hover {
  color: #ffff;
  transition: background-color .5s;
}

#btnEdit:hover {
  background: #99B2CA;
}

#btnDelete:hover {
  background: #F17D7D;
}

#inputSave {
  background: #EAEAEA;
  border-radius: 2px;
  width: 100%;
  height: 48px;
  border-style: none;
  font-size: 24px;
  box-sizing: border-box;
  margin-bottom: 14px;
  
}

form {
  display: flex;
  justify-content: space-between;
}

#btnSave { 
  background: transparent;
  margin-right: 18px;
}

#btnSave:hover {
  background: #99B2CA;
}
</style>