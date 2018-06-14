<template>
	<section class="todo-active">
			<h2>タスク一覧</h2>
			<ul class="todo_list">
				<li class="todo" v-for="(todo, index) in todos">
						{{todo.task}} <button v-on:click="done(index)">完了</button>
				</li>
			</ul>
	</section>
</template>

<script>
  export default {
    name: 'active-todo',
    props: ['todos'],
    methods: {
      done (id) {
        this.$emit('done', id)
      }
    }
  }
</script>

<style>
</style>
