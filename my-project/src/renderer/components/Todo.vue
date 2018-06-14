<template>
  <div>
    <section class="todo_form">
      <p>Todoを入力してください</p>
      <input v-model="new_task" type="text" class="todo_form_field">
      <button v-on:click="add()">作成</button>
    </section>
    <active-todo :todos="active_todos" v-on:done="done"></active-todo>
    <done-todo :todos="done_todos"></done-todo>
  </div>
</template>

<script>
  import ActiveTodo from './ActiveTodo.vue'
  import DoneTodo from './DoneTodo.vue'
  export default {
    name: 'todo-page',
    components: {
      ActiveTodo,
      DoneTodo
    },
    data: function () {
      return {
        new_task: null,
        active_todos: [],
        done_todos: []
      }
    },
    methods: {
      open (link) {
        this.$electron.shell.openExternal(link)
      },
      add: function () {
        var _this = this
        var newTodo = {
          task: _this.new_task,
          isChecked: false
        }
        this.active_todos.push(newTodo)
        this.new_task = null
      },
      done: function (id) {
        var doneTodo = this.active_todos.splice(id, 1)
        this.done_todos.push(doneTodo[0])
      }
    }
  }
</script>

<style>

</style>
