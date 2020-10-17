<template>
	<div class="heroSection row justify-content-center mt-5">
		<h1>{{ welcomeMessage }}</h1>
	</div>
</template>

<script>
	export default {
		name: "HeroSection",
		props: {
			welcomeMessage: String,
		},
	};
</script>
