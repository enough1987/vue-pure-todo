
<template>
  <div>
    <App-add-todo>
    </App-add-todo>
    <App-todos-list
      :todos="todos"
    >
    </App-todos-list>
  </div>
</template>

<script>
import AppTodosList from './AppTodosList'
import AppAddTodo from './AppAddTodo'

export default {
  name: 'app-todos',
  components: {
    'App-add-todo': AppAddTodo,
    'App-todos-list': AppTodosList
  },
  data () {
    return {
      todos: [
        {
          id: 0,
          name: 'test',
          author: 'test'
        }
      ]
    }
  },
  methods: {
    addTodo (todo) {
      console.log('add', todo)
      const id = this.todos.reduce((id, todo) => {
        if (todo.id === id || todo.id > id) {
          return todo.id + 1
        }
        return id
      }, 0)

      this.todos = [...this.todos, { ...todo, id }]
    },
    updateTodo (todo) {
      console.log('upadete', todo)
      this.todos = this.todos.map(_todo => Object.is(_todo, todo) ? {...todo} : _todo)
      console.log(this.todos)
    },
    removeTodo (todo) {
      console.log('remove', todo)
      this.todos = this.todos.filter(_todo => _todo.id !== todo.id)
    },
    validateTodo (todo) {
      if (!todo.name || !todo.author) {
        return false
      }
      return true
    }
  },
  provide: function () {
    return {
      addTodo: this.addTodo,
      updateTodo: this.updateTodo,
      removeTodo: this.removeTodo,
      validateTodo: this.validateTodo
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
