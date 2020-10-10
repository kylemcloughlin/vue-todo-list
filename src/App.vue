<template>
<div id="app">
  <Todos v-bind:todos="todos" @updatecompleted="updatedata"/>

</div>
</template>

<script>
import Todos from './components/Todos';
console.log('hit');
export default {
  name: 'App',
  components: {
    Todos
  },
  data() {
    return {
      todos: [
        {
          id:1,
          title: 'Todo one',
          completed: false
        },
        {
          id:2,
          title: 'Todo two',
          completed: true
        },
        {
          id:3,
          title: 'Todo three',
          completed: false
        },
      ]
    }
  },
  methods: {
    updatedata(id) {
      this.todos[id-1].completed = !this.todos[id-1].completed;

    }
  }
}
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
