<template>
  <div id="todo-list">
    <div class="todo-container">
      <div class="todo-wrap">
        <TodoListHeader ref="todoListHeader" />
        <TodoListBody :todos="todos" />
        <TodoListFooter ref="todoListFooter" :todos="todos" />
      </div>
    </div>
  </div>
</template>

<script>
import { nanoid } from 'nanoid'
import TodoListHeader from './TodoListHeader.vue'
import TodoListBody from './TodoListBody.vue'
import TodoListFooter from './TodoListFooter.vue'

export default {
  name: 'TodoList',
  components: { TodoListHeader, TodoListBody, TodoListFooter },
  data() {
    return {
      todos: [],
    }
  },
  methods: {
    addTodo(title) {
      const todo = {
        id: nanoid(),
        title,
        done: false,
      }
      this.todos.unshift(todo)
    },
    del(id) {
      this.todos.splice(
        this.todos.findIndex((todo) => todo.id === id),
        1
      )
    },
    isDone(id, value) {
      this.todos[this.todos.findIndex((todo) => todo.id === id)].done = value
    },
    delDone() {
      this.todos = this.todos.filter((todo) => todo.done === false)
    },
    checkAll(value) {
      this.todos.forEach((todo) => (todo.done = value))
    },
  },
  mounted() {
    this.$refs.todoListHeader.$on('addTodo', this.addTodo)
    this.$refs.todoListFooter.$on('delDone', this.delDone)
    this.$refs.todoListFooter.$on('checkAll', this.checkAll)
    this.$bus.$on('deleteTodo', this.del)
    this.$bus.$on('isDone', this.isDone)
  },
  beforeDestroy() {
    this.$refs.todoListHeader.$off('addTodo')
    this.$refs.todoListFooter.$off(['delDone', 'checkAll'])
    this.$bus.$off(['deleteTodo', 'isDone'])
  },
}
</script>

<style scoped>
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>