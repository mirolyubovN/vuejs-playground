<template>
	<div>
		<h2>Todo list app</h2>
		<hr>
		<router-link to='/'>Homepage</router-link>
		<AddTodo
			@addTodo="addTodo"
		/>
		<TodoList
			v-bind:todos="todos"
			@removeTodo="removeTodo"
		/>
	</div>
</template>

<script>
import TodoList from '@/components/TodoList.vue';
import AddTodo from '@/components/AddTodo.vue';

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
	mounted() {
		fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
			.then((response) => response.json())
			.then((json) => {
				this.todos = json;
			});
	},
	components: {
		TodoList,
		AddTodo,
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
