<template>
  <div>
    <div v-bind:key="todo.id" v-for="todo in todos">
      <TodoItem v-bind:todo="todo" @updatecompleted="setCompleted" v-on:del-todo="$emit('del-todo', todo.id)"/>
    </div>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';
export default {
  name: "Todos",
  components: {
      TodoItem
  },
  props:["todos"],
  methods: {
      setCompleted(id) {
          this.$emit('updatecompleted', id); ///you need to reed documentation on $emit
    }
  }
}
 

</script>

<style scoped>
</style>
