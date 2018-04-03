<!-- Fix still needed: delete removes item above not current item -->
<template>
  <div id="app" class="container">
    <h1>To Do App</h1>
    <form @submit.prevent="addTodo()">
  <div class="form-group">
    <label for="newTodo">New To Do</label>
    <input v-model="newTodo" type="text" class="form-control" id="newTodo" aria-describedby="newTodoHelp" placeholder="Walk the dog...">
    <small id="newTodoHelp" class="form-text text-muted">Enter a new to  do.</small>
  </div>
   <button type="submit" class="btn btn-primary">Add To Do</button>
    </form>
    <ul class="list-group mt-3">
    <li v-for="todo, i in todos" class="list-group-item">
     <button
      @click="markDone(todo)"
      v-if="!todo.done"
      type="button"
      class="btn btn-primary">done</button>
      <button
      @click="remove(todo)"
      type="button"
      class="btn btn-danger">Delete</button>
      <span :class= "{
        isDone: todo.done
        }"
        >{{todo.title}}</span>
    </li>
  
  </ul>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      newTodo: "",
      todos: []
    }
  },
  watch: {
    todos: {
      handler() {
        localStorage.todos=JSON.stringify(this.todos)
      },
      deep: true
    }
  },
  mounted() {
    if(localStorage.todos) {
      this.todos=JSON.parse(localStorage.todos)
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
    markDone(todo) {
      todo.done = true
    },
    remove(index) {
      this.todos.splice(index, 1)
    }
  }
}

</script>

<style>

.isDone {
  text-decoration: line-through;
}

</style>
