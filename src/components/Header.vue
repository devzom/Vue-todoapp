<template>
	<div id="nav" class="">
		<router-link to="/">Home</router-link> |
		<router-link to="/about">About</router-link>
	</div>
</template>

<script>
	export default {
		name: "Header",
	};
</script>

<style scoped>
	#nav {
		padding: 50px;
	}

	#nav a {
		font-weight: bold;
		color: #2c3e50;
	}

	#nav a.router-link-exact-active {
		color: #ffc107;
	}
	#nav a:hover {
		color: #ffc107;
		text-decoration: none;
	}

	ul {
		list-style-type: none;
		padding: 0;
	}
	li {
		display: inline-block;
		margin: 0 10px;
	}
</style>
