<template>
	<div class="home">
		<HeroSection welcomeMessage="Let's start Your day with a list" />
		<TodoList />
	</div>
</template>

<script>
	// @ is an alias to /src
	import HeroSection from "@/components/HeroSection.vue";
	import TodoList from "@/components/TodoList.vue";

	export default {
		name: "Home",
		components: {
			HeroSection,
			TodoList,
		},
	};
</script>
