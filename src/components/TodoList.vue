<template>
	<div class="container align-content-center justify-content-center mt-5 todo">
		<div class="row mb-4">
			<TodoAddForm v-on:add-todo="addNewTodo" />
		</div>
		<div class="row">
			<div class="col-4 border-right todo__title mt-5">
				<h4><b-icon icon="list-task"></b-icon> Things to do:</h4>
				<div class="todo__statistic pt-4">
					<p class="text-danger">To do: {{ undoneTodo }}</p>
					<p class="text-success">Done: {{ doneTodo }}</p>
				</div>
			</div>
			<div class="col-8 text-left mt-5 todo__itemsContainer">
				<ul>
					<li class="todo__item" :class="{ 'todo__item--done': todo.status == 1 }" v-for="todo in sortTodoItems" :key="todo.id">
						<TodoItem :todo="todo" v-on:del-todo="deleteTodo" v-on:toggle-todo="countTodos" />
					</li>
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
	import TodoItem from "@/components/TodoItem.vue";
	import TodoAddForm from "@/components/TodoAddForm.vue";

	export default {
		name: "TodoList",
		components: {
			TodoItem,
			TodoAddForm,
		},
		data() {
			return {
				dataList: [],
				doneTodo: 0,
				undoneTodo: 0,
			};
		},
		methods: {
			countTodos() {
				this.undoneTodo = this.dataList.filter((todo) => todo.status == 0).length;
				this.doneTodo = this.dataList.filter((todo) => todo.status == 1).length;
			},
			addNewTodo(newTodoItem) {
				this.dataList = [...this.dataList, newTodoItem];
				this.countTodos();
			},
			deleteTodo(id) {
				// first delete selected item and then count the list again
				this.dataList = this.dataList.filter((todo) => todo.id !== id);
				this.countTodos();
			},
		},
		created() {
			const testData = {
				id: 1,
				content: "Sample task (hard coded in todoList:data)",
				status: 0,
			};
			this.dataList = [...this.dataList, testData];
		},
		mounted() {
			this.countTodos();
		},
		computed: {
			sortTodoItems: function() {
				return this.dataList.slice().sort(function(a, b) {
					//reverse id sorting => 4,3,2,1
					return a.id < b.id ? 1 : -1;
				});
			},
		},
	};
</script>

<style lang="scss" scoped>
	.todo {
		padding: 20px 40px;

		li {
			list-style-type: none;
		}

		&__list {
			padding-top: 20px;
		}

		&__itemsContainer {
			max-height: 50vh;
			overflow-y: auto;
		}

		&__item {
			font-size: 1.3rem;
			line-height: 2.5rem;
			letter-spacing: 0.1rem;

			&--done {
				color: #42b983;
				text-decoration: line-through;
			}
		}

		&__statistic {
			font-size: 1.4rem;
		}
	}
</style>
