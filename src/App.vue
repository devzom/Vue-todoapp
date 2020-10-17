<template>
	<div id="app">
		<div class="container">
			<Header />
			<router-view />
		</div>
	</div>
</template>

<script>
	import Header from "@/components/Header.vue";
	export default {
		components: {
			Header,
		},
	};
</script>

<style lang="scss">
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
	}

	a {
		color: #ffc107;
	}

	h1,
	h2,
	h3,
	h4,
	h5,
	h6 {
		color: #ffc107;
	}
</style>
