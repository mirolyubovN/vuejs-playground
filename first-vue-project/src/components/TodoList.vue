<template>
	<div>
		<ul>
			<TodoItem
				v-on:removeTodo="removeTodo"
				v-for="(todo, i) of todos"
				:index="i"
				:todo="todo"
				:key="todo.id"
			/>
		</ul>
	</div>
</template>

<script>
import TodoItem from '@/components/TodoItem.vue';

export default {
	props: ['todos'],
	name: 'App',
	components: {
		TodoItem,
	},
	methods: {
		removeTodo(id) {
			this.$emit('removeTodo', id);
		},
	},
};
</script>

<style scoped>
	ul {
		list-style: none;
		padding: 0;
		margin: 0;
	}
</style>
