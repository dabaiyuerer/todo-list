<template>
  <div id="app">
    <TodoList />
  </div>
</template>

<script>
import TodoList from './components/todolist/TodoList.vue'

export default {
  name: 'App',
  components: { TodoList },
}
</script>

<style>
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-edit {
  margin-right: 6px;
  color: #fff;
  background-color: #69d469;
  border: 1px solid #499849;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}
.btn-edit:hover {
  color: #fff;
  background-color: #499849;
}

.btn:focus {
  outline: none;
}
</style>
