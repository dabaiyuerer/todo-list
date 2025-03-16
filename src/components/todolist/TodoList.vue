<template>
  <div id="todo-list">
    <div class="todo-container">
      <div class="todo-wrap">
        <TodoListHeader />
        <TodoListBody />
        <TodoListFooter />
      </div>
    </div>
  </div>
</template>

<script>
import TodoListHeader from './TodoListHeader.vue'
import TodoListBody from './TodoListBody.vue'
import TodoListFooter from './TodoListFooter.vue'

export default {
  name: 'TodoList',
  components: { TodoListHeader, TodoListBody, TodoListFooter },
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