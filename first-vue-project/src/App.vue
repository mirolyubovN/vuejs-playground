<template>
	<div id="app">
		<h1>Todo list app</h1>
		<hr>
		<TodoList
			v-bind:todos="todos"
			@removeTodo="removeTodo"
		/>
	</div>
</template>

<script>
import TodoList from '@/components/TodoList.vue';

export default {
	name: 'App',
	data() {
		return {
			todos: [
				{ id: 1, title: 'Explore VueJS', completed: false },
				{ id: 2, title: 'Make todo app', completed: false },
				{ id: 3, title: 'Have a cup of coffee', completed: false },
				{ id: 4, title: 'Enjoy the rest of the day', completed: false },
			],
		};
	},
	components: {
		TodoList,
	},
	methods: {
		removeTodo(id) {
			this.todos = this.todos.filter((item) => item.id !== id);
		},
	},
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
