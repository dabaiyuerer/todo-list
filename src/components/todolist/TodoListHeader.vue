<template>
  <div class="todo-header">
    <input
      type="text"
      placeholder="请输入你的任务名称，按回车键确认"
      @keyup.enter="addTodo"
      ref="headerInput"
    />
  </div>
</template>

<script>
export default {
  name: 'TodoListHeader',
  methods: {
    addTodo() {
      if (!this.$refs.headerInput.value.trim()) {
        confirm('待办事件内容不能为空！')
      } else {
        this.$emit('addTodo', this.$refs.headerInput.value.trim())
      }
      this.$refs.headerInput.value = ''
    },
  },
}
</script>

<style scoped>
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
</style>
