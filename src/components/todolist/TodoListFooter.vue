<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" v-model="checkAll" />
    </label>
    <span>
      <span>已完成{{ hasDone }}</span> / 全部{{ total }}
    </span>
    <button class="btn btn-danger" @click="delDone">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: 'TodoListFooter',
  props: ['todos'],
  methods: {
    delDone() {
      this.$emit('delDone')
    },
  },
  computed: {
    hasDone() {
      return this.todos.reduce((prev, curr) => prev + (curr.done ? 1 : 0), 0)
    },
    total() {
      return this.todos.length
    },
    checkAll: {
      get() {
        return this.total > 0 && this.hasDone === this.total
      },
      set(value) {
        this.$emit('checkAll', value)
      },
    },
  },
}
</script>

<style scoped>
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>