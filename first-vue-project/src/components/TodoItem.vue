<template>
	<li>
		<span v-bind:class="{ done: todo.completed }">
			<input type="checkbox"
					v-on:change="todo.completed = !todo.completed"
					v-bind="{ checked: todo.completed }">
			<strong>{{ index+1 }}</strong>
			{{ todo.title | upperCase }}
		</span>
		<button class="rm"
				v-on:click="$emit('removeTodo', todo.id)">
			&times;
		</button>
	</li>
</template>

<script>
export default {
	props: {
		todo: {
			type: Object,
			required: true,
		},
		index: Number,
	},
	filters: {
		upperCase(value) {
			return value.charAt(0).toUpperCase() + value.slice(1);
		},
	},
};
</script>

<style scoped>
	li {
		border: 1px solid tomato;
		display: flex;
		justify-content: space-between;
		padding: .5rem 2rem;
		margin-bottom: 1rem;
	}
	.rm {
		background: red;
		color: #fff;
		border-radius: 50%;
		font-weight: bold;
		border: none;
	}
	input {
		margin-right: 1rem;
	}
	.done {
		text-decoration: line-through;
	}
</style>
