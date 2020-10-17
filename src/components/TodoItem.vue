// 'todo' single item it's getting TodoItem data from TodoList by props
<template>
	<div class="card mb-3">
		<div class="card-body row flex-row justify-content-start align-items-center">
			<div class="col-1">
				<input class="checkbox checkbox-success" type="checkbox" @change="toggleTodo()" />
			</div>
			<div class="col-9">
				<p>{{ todo.content }}</p>
			</div>
			<div class="col-2">
				<button type="button" class="btn btn-outline-danger" @click="$emit('del-todo', todo.id)"><b-icon-trash></b-icon-trash></button>
			</div>
			<strong>{{ status }}</strong>
		</div>
	</div>
</template>

<script>
	export default {
		name: "TodoItem",
		props: {
			todo: Object,
		},
		data() {
			return {
				status: "",
			};
		},
		methods: {
			toggleTodo: function() {
				this.todo.status = !this.todo.status;
				this.$emit("toggle-todo", this.todo.id);
			},
		},
	};
</script>

<style>
	::selection {
		background-color: transparent;
	}
</style>
