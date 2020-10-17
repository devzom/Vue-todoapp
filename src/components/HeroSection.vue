<template>
	<div class="heroSection container mt-3">
		<div class="row justify-content-center">
			<h1>{{ welcomeMessage }}</h1>
		</div>
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
