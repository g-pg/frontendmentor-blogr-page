<script>
import Footer from "./Footer.vue";
import Header from "./Header.vue";

export default {
	components: {
		Footer,
		Header,
	},
};
</script>

<template>
	<Header />
	<main>
		<slot></slot>
	</main>
	<Footer />
</template>

<style></style>
