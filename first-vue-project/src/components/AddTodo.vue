<template>
	<form @submit.prevent="onSubmit">
		<input type="text" v-model="title">
		<button type="submit">Add todo item</button>
	</form>
</template>

<script>
export default {
	data() {
		return {
			title: '',
		};
	},
	methods: {
		onSubmit() {
			console.log(this.title);
			if (this.title.trim()) {
				const newTodoItem = {
					id: Date.now(),
					title: this.title,
					completed: false,
				};

				this.$emit('addTodo', newTodoItem);
				this.title = '';
			}
		},
	},
};
</script>

<style scoped>
	form {
		display: flex;
		margin-bottom: 2rem;
	}
	input {
		width: 400px;
	}
</style>
