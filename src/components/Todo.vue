<template>
  <div>
    <form @submit.prevent="addTodo">
      <label for="newTodo">New Todo</label>
      <input type="text" name="newTodo" id="newTodo" value="" v-model="newTodo" />
      <button type="submit" name="Button">Add</button>
    </form>
    <button type="button" @click="allDone">All Done</button>
    <ul>
      <li v-for="todo in todos" :key="todo">
        <input type="checkbox" v-model="todo.done" />
        <span :class="{ done: todo.done }">{{todo.title}}</span>
        <button name="Remove" @click="removeTodo(todo)">Remove</button>
        </li>
    </ul>
  </div>
</template>

<script>
require('@/assets/css/main.css')

export default {
  name: 'Todo',
  data() {
    return {
      newTodo: '',
      todos: []
    }
  }, 
  methods: {
    addTodo() {
      this.todos.push({
        title: this.newTodo,
        done: false
      })

      this.newTodo = ''
    },
    removeTodo(todo) {
      const indexTodo = this.todos.indexOf(todo)
      this.todos.splice(indexTodo, 1)
    }, 
    allDone() {
      this.todos.forEach(todo => {
        todo.done = true
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.done {
  text-decoration: line-through;
}
</style>
