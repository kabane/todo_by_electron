<template>
	<section class="todo-done">
      <h2>完了タスク</h2>
      <ul class="todo_list">
        <li class="todo" v-for="todo in todos">
          {{todo.task}}
        </li>
      </ul>
    </section>
</template>

<script>
  export default {
    name: 'done-todo',
    props: ['todos']
  }
</script>

<style>
</style>
