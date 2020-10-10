<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" v-bind:todos="todos" />
    <Todos v-bind:todos="todos" @updatecompleted="updatedata" @del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";
import Header from "./components/layout/header.vue";
import axios from 'axios';
console.log("hit");
export default {
  name: "App",
  components: {
    Header,
    AddTodo,
    Todos
  },
  data() {
    return {
      todos: [

       ]
    };
  },
  methods: {
    updatedata(id) {
      for (let x in this.todos) {
        if (this.todos[x].id === id) {
          this.todos[x].completed = !this.todos[x].completed;
          console.log("hitboyhitboy", id);
        }
      }
    },

    deleteTodo(id) {
   axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
   .then(res => console.log(res))
    .catch(err=> console.log(err))

    this.todos = this.todos.filter(todo => {
        return todo.id !== id;
      });

      // console.log( this.todos[id - 1])
    },
    addTodo(newTodo) {
     const {  title,completed} = newTodo 
         axios.post('https://jsonplaceholder.typicode.com/todos', {
           title,
           completed
         })
    .then(res => this.todos = [...this.todos, res.data] )
    .catch(err=> console.log(err))
  
    }
  
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
    .then(res => this.todos =res.data )
    .catch(err=> console.log(err))
  }
  
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
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
  background: #666;
}
</style>
