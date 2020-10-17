// 'todo' single item it's getting TodoItem data from TodoList by props
<template>
	<div class="card mb-3">
		<div class="card-body">
			<div class="row flex-row justify-content-start align-items-center">
				<div class="col-10 p-0 d-inline-block">
					<input class="checkbox mx-2" type="checkbox" @change="toggleTodo()" />
					{{ todo.content }}
				</div>
				<div class="col-2 mr-0 pr-0">
					<button type="button" class="btn btn-outline-danger" @click="$emit('del-todo', todo.id)"><b-icon-trash></b-icon-trash></button>
				</div>
			</div>
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
