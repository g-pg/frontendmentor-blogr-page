<script>
import Nav from "./Nav.vue";
import PrimaryBtn from "./PrimaryBtn.vue";

export default {
	components: {
		Nav,
		PrimaryBtn,
	},
};
</script>

<template>
	<header>
		<Nav />
		<div class="container">
			<div class="content">
				<h1 class="title">A modern publishing platform</h1>
				<h2 class="subtitle">Grow your audience and build your online brand</h2>

				<div class="btns">
					<PrimaryBtn content="Start for Free" filled />
					<PrimaryBtn content="Learn More" hollow />
				</div>
			</div>
		</div>
	</header>
</template>

<style scoped>
header {
	background: url("../assets/bg-pattern-intro-desktop.svg"), var(--red-bg);
	background-position: 10% 50%;
	height: 100dvh;
	padding-block: 3rem;
	display: flex;
	flex-direction: column;
	border-radius: 0 0 0 90px;
	position: relative;
	z-index: 1;
	/* margin-bottom: 5rem; */
}

@media (max-width: 700px) {
	header {
		background: url("../assets/bg-pattern-intro-mobile.svg"), var(--red-bg);
		background-position: 30% 40%;
	}
}
.container {
	display: grid;
	place-items: center;
	height: 100%;
}
.content {
	display: flex;
	flex-direction: column;
	align-items: center;
	gap: 0.5rem;
	z-index: 2;
}

.title,
.subtitle {
	font-family: var(--overpass);
	color: var(--white);
	text-align: center;
}

.title {
	font-size: clamp(2rem, 10vw, 4rem);
	font-weight: 600;
}

.subtitle {
	font-size: clamp(0.8rem, 5vw, 1.3rem);
	font-weight: 300;
}

.btns {
	display: flex;
	align-items: center;
	gap: 1rem;
	margin-top: 3rem;
}

@media (max-width: 980px) {
}
</style>
