<template>
  <ul class="todo-main">
    <TodoListItem />
  </ul>
</template>

<script>
import TodoListItem from './TodoListItem.vue'

export default {
  name: 'TodoListBody',
  components: { TodoListItem },
}
</script>

<style scoped>
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>