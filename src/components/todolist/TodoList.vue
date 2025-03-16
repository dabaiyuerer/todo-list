<template>
  <div id="todo-list">
    <div class="todo-container">
      <div class="todo-wrap">
        <TodoListHeader ref="todoListHeader" />
        <TodoListBody :todos="todos" />
        <TodoListFooter />
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
  },
  mounted() {
    this.$refs.todoListHeader.$on('addTodo', this.addTodo)
  },
  beforeDestroy() {
    this.$refs.todoListHeader.$off('addTodo')
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