<template>
  <li>
    <label>
      <input type="checkbox" v-model="isDone" />
      <span v-show="isShow">{{ todo.title }}</span>
      <input
        v-show="!isShow"
        type="text"
        v-model="editTodoTitle"
        ref="inputTitle"
        @blur="saveEdit"
      />
    </label>
    <button class="btn btn-danger" @click="deleteTodo">删除</button>
    <button v-show="canEdit" class="btn btn-edit" @click="editTodo">
      编辑
    </button>
  </li>
</template>

<script>
export default {
  name: 'TodoListItem',
  props: ['todo'],
  data() {
    return {
      isShow: true,
      canEdit: !this.todo.done,
    }
  },
  watch: {
    todo: {
      deep: true,
      handler() {
        this.canEdit = !this.todo.done
      },
    },
  },
  methods: {
    deleteTodo() {
      this.$bus.$emit('deleteTodo', this.todo.id)
    },
    editTodo() {
      this.isShow = !this.isShow
      this.canEdit = false
      this.$nextTick(function () {
        this.$refs.inputTitle.focus()
      })
    },
    saveEdit() {
      this.isShow = !this.isShow
      this.canEdit = true
    },
  },
  computed: {
    isDone: {
      get() {
        return this.todo.done
      },
      set(value) {
        this.$bus.$emit('isDone', this.todo.id, value)
      },
    },
    editTodoTitle: {
      get() {
        return this.todo.title
      },
      set(value) {
        if (value.trim()) this.$bus.$emit('editTodoTitle', this.todo.id, value)
      },
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