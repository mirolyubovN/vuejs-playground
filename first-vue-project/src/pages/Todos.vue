<template>
	<div>
		<h2>Todo list app</h2>
		<hr>
		<router-link to='/'>Homepage</router-link>
		<AddTodo
			@addTodo="addTodo"
		/>
		<Loader v-if="loading" />
		<TodoList
			v-else-if="todos.length"
			v-bind:todos="todos"
			@removeTodo="removeTodo"
		/>
		<p v-else>
			Seems like you've done everything. If you are feeling productive today,
			you can add a few more todos using the form above
		</p>
	</div>
</template>

<script>
import TodoList from '@/components/TodoList.vue';
import AddTodo from '@/components/AddTodo.vue';
import Loader from '@/components/Loader.vue';

export default {
	name: 'App',
	data() {
		return {
			todos: [],
			loading: true,
		};
	},
	mounted() {
		fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
			.then((response) => response.json())
			.then((json) => {
				setTimeout(() => {
					this.todos = json;
					this.loading = false;
				}, 1000);
			});
	},
	components: {
		TodoList,
		AddTodo,
		Loader,
	},
	methods: {
		removeTodo(id) {
			this.todos = this.todos.filter((item) => item.id !== id);
		},
		addTodo(todoItem) {
			this.todos.push(todoItem);
		},
	},
};
</script>
