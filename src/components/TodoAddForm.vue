<template>
	<div class="">
		<div v-if="alertStatus" class="alert alert-warning alert-dismissible fade show m-4" role="alert">
			<strong>Input is empty, please fill it to make Your day easier. ;)</strong>
		</div>
		<sweetalert-icon v-if="showSuccessEffect" icon="success"></sweetalert-icon>
		<form @submit="createTodoItem">
			<div class="form-row align-items-center justify-content-end m-0 p-0">
				<div class="col-10">
					<input
						type="text"
						class="form-control"
						v-model="content"
						name="content"
						placeholder="Any plans? Make a todo..."
						aria-label="Write content of your to do task"
					/>
				</div>
				<div class="col-2">
					<button type="submit" class="btn btn-dark">Add <b-icon-plus></b-icon-plus></button>
				</div>
			</div>
		</form>
	</div>
</template>

<script>
	import uuid from "uuid";

	export default {
		name: "TodoAddForm",
		data() {
			return {
				content: "",
				alertStatus: false,
				showSuccessEffect: false,
			};
		},
		methods: {
			createTodoItem(e) {
				//prevent defualt SUBMIT event of page causing reloading page and trying to send it to a server
				e.preventDefault();
				//check if input field is not empty
				if (this.content != "") {
					const newTodoItem = {
						id: uuid.v4(),
						content: this.content,
						status: 0,
					};
					console.log("createTodoItem -> newTodoItem", newTodoItem);

					//send to parent = todoList by $emit
					this.$emit("add-todo", newTodoItem);

					//clear input field after form is sent
					this.content = "";

					//show success alert icon
					this.showSuccessEffect = true;
					setTimeout(() => {
						this.showSuccessEffect = false;
					}, 1500);
				} else {
					console.log("form is empty! fill it");
					this.toggleAlert();
				}
			},
			toggleAlert() {
				if (!this.content && !this.alertStatus) {
					this.alertStatus = !this.alertStatus;
					setTimeout(() => {
						this.alertStatus = false;
					}, 1500);
				}
			},
		},
	};
</script>
