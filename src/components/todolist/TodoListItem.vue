<template>
  <li>
    <label>
      <input type="checkbox" />
      <span>{{ todo.title }}</span>
    </label>
    <button class="btn btn-danger" @click="deleteTodo">删除</button>
  </li>
</template>

<script>
export default {
  name: 'TodoListItem',
  props: ['todo'],
  methods: {
    deleteTodo() {
      this.$bus.$emit('deleteTodo', this.todo.id)
    },
  },
}
</script>

<style scoped>
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:hover button {
  display: inline-block;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}
</style>