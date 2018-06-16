<template>
  <div>
    <section class="todo_form">
      <p>Todoを入力してください</p>
      <input v-model="new_task" type="text" class="todo_form_field">
      <button v-on:click="add()">作成</button>
    </section>
    <section class="todo-active">
			<h2>タスク一覧</h2>
			<ul class="todo_list">
				<li class="todo" v-for="(todo, index) in todos" :key="todo.id">
          <todo :todo="todo"></todo>
				</li>
			</ul>
	</section>
  </div>
</template>

<script>
  import Todo from './Todo.vue'
  export default {
    name: 'todo-app',
    components: {
      Todo
    },
    data: function () {
      return {
        new_task: '',
        todos: []
      }
    },
    methods: {
      open (link) {
        this.$electron.shell.openExternal(link)
      },
      add: function () {
        var _this = this
        var newTodo = {
          id: _this.todos.length,
          name: _this.new_task,
          elapsed_time: 0,
          is_active: true
        }
        this.todos.push(newTodo)
        this.new_task = null
      },
      done: function () {
        // var doneTodo = this.todos.splice(id, 1)
        // this.todos.push(doneTodo[0])
      }
    }
  }
</script>

<style>

</style>
