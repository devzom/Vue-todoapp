<template>
	<div class="col-12">
		<div class="sweetAlertIconBox">
			<sweetalert-icon v-if="showSuccessEffect" icon="success"></sweetalert-icon>
		</div>
		<div v-if="alertStatus" class="alert alert-warning fade show" role="alert">
			<strong>Input is empty, please fill task content</strong>
		</div>
		<form class="row text-right d-flex justify-content-end" @submit="createTodoItem">
			<div class="col-10 m-0">
				<input
					type="text"
					class="form-control m-0 pl-4"
					v-model="content"
					name="content"
					placeholder="Any plans? Make a todo..."
					aria-label="Write content of your to do task"
				/>
			</div>
			<div class="col-1">
				<button type="submit" class="btn btn-dark m-0"><b-icon-plus></b-icon-plus></button>
			</div>
		</form>
	</div>
</template>

<script>
	// import uuid from "uuid";

	export default {
		name: "TodoAddForm",
		data() {
			return {
				content: "",
				alertStatus: false,
				showSuccessEffect: false,
				todoId: 2,
			};
		},
		methods: {
			createTodoItem(e) {
				//prevent defualt SUBMIT event of page causing reloading page and trying to send it to a server
				e.preventDefault();
				//check if input field is not empty
				if (this.content != "") {
					const newTodoItem = {
						id: this.todoId,
						// id: uuid.v4(),
						content: this.content,
						status: 0,
					};
					console.log("createTodoItem -> newTodoItem", newTodoItem);

					//send to parent = todoList by $emit
					this.$emit("add-todo", newTodoItem);

					//clear input field after form is sent
					this.content = "";
					this.todoId++;

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

<style scoped>
	/* show alert icon on top-right corner od todoItem card */
	.sweetAlertIconBox {
		height: 80px;
		width: 80px;
		position: absolute;
		top: 45px;
		right: 10px;
		z-index: 10;
	}
</style>
