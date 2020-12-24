<template>
	<div>
		<h2>Todo list app</h2>
		<hr>
		<router-link to='/'>Homepage</router-link>
		<AddTodo
			@addTodo="addTodo"
		/>
		<select v-model="filter">
			<option value="all">All</option>
			<option value="completed">Completed</option>
			<option value="incomplete">Not yet completed</option>
		</select>
		<hr>
		<Loader v-if="loading" />
		<TodoList
			v-else-if="filteredTodos.length"
			v-bind:todos="filteredTodos"
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
			filter: 'all',
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
	watch: {
		filter(value) {
			console.log(value);
		},
	},
	computed: {
		filteredTodos() {
			if (this.filter === 'all') {
				return this.todos;
			}
			if (this.filter === 'completed') {
				return this.todos.filter((todo) => todo.completed);
			}
			if (this.filter === 'incomplete') {
				return this.todos.filter((todo) => !todo.completed);
			}
			return null;
		},
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
