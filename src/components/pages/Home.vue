<script>
import PageLayout from "../PageLayout.vue";
import Header from "../Header.vue";
import Footer from "../Footer.vue";

export default {
	components: {
		PageLayout,
		Header,
		Footer,
	},
	data() {
		return {
			windowWidth: window.innerWidth,
		};
	},
	mounted() {
		window.addEventListener("resize", this.handleWindowResize);
	},
	beforeUnmount() {
		window.removeEventListener("resize", this.handleWindowResize);
	},
	methods: {
		updateWindowWidth() {
			this.windowWidth = window.innerWidth;
		},
	},
	computed: {
		isMobile() {
			return this.windowWidth <= 980;
		},
	},
};
</script>

<template>
	<PageLayout>
		<Header />
		<section class="editor-section">
			<div class="container">
				<div class="editor-section-wrapper">
					<h2 class="section-title blue">Designed for the future</h2>
					<div class="equal-columns">
						<div class="text-column">
							<div class="text-segment">
								<h3>Introducing an extensible editor</h3>
								<p>
									Blogr features an exceedingly intuitive interface which
									lets you focus on one thing: creating content. The
									editor supports management of multiple blogs and allows
									easy manipulation of embeds such as images, videos, and
									Markdown. Extensibility with plugins and themes provide
									easy ways to add functionality or change the looks of a
									blog.
								</p>
							</div>
							<div class="text-segment">
								<h3>Robust content management</h3>
								<p>
									Flexible content management enables users to easily
									move through posts. Increase the usability of your blog
									by adding customized categories, sections, format, or
									flow. With this functionality, you’re in full control.
								</p>
							</div>
						</div>
						<div class="img-column">
							<img
								src="../../assets/illustration-editor-desktop.svg"
								alt="Design sketch with scribbled lines, circles and squares"
								class="editor-img"
							/>
						</div>
					</div>
				</div>
			</div>
		</section>
		<section class="phones-section">
			<div class="container">
				<div class="phones-section-wrapper">
					<div class="equal-columns">
						<div class="img-column">
							<img
								src="../../assets/illustration-phones.svg"
								alt="Design sketch with scribbled lines, circles and squares"
								class="phones-img"
							/>
						</div>
						<div class="text-column">
							<h2>State of the Art Infrastructure</h2>
							<p>
								With reliability and speed in mind, worldwide data centers
								provide the backbone for ultra-fast connectivity. This
								ensures your site will load instantly, no matter where your
								readers are, keeping your site competitive.
							</p>
						</div>
					</div>
				</div>
			</div>
		</section>
		<section class="laptop-section">
			<div class="container">
				<div class="laptop-section-wrapper">
					<div class="equal-columns">
						<div class="img-column">
							<img
								src="../../assets/illustration-laptop-desktop.svg"
								alt="Laptop with a website layout on the screen"
								class="laptop-img"
							/>
						</div>
						<div class="text-column">
							<div class="text-segment">
								<h3>Free, open, simple</h3>
								<p>
									Blogr is a free and open source application backed by a
									large community of helpful developers. It supports
									features such as code syntax highlighting, RSS feeds,
									social media integration, third-party commenting tools,
									and works seamlessly with Google Analytics. The
									architecture is clean and is relatively easy to learn.
								</p>
							</div>
							<div class="text-segment">
								<h3>Powerful tooling</h3>
								<p>
									Batteries included. We built a simple and
									straightforward CLI tool that makes customization and
									deployment a breeze, but capable of producing even the
									most complicated sites.
								</p>
							</div>
						</div>
					</div>
				</div>
			</div>
		</section>
		<Footer />
	</PageLayout>
</template>

<style scoped>
section {
	margin-block: 10rem;
}
.section-title {
	color: var(--very-dark-blue);
	text-align: center;
	font-size: clamp(1.2rem, 10vw, 2rem);
	font-weight: 500;
}
.editor-section-wrapper,
.laptop-section-wrapper {
	position: relative;
	/* padding-block: 5rem; */
	width: 80%;
	margin: 0 auto;
	min-height: 90vh;
}
.editor-section .equal-columns,
.laptop-section .equal-columns {
	margin-top: 3rem;
	display: flex;
	align-items: center;
	height: 100%;
	gap: 5rem;
	margin-top: 5rem;
}

.editor-section .equal-columns > div,
.laptop-section .equal-columns > div {
	flex-basis: 100%;
}

.editor-section .text-column,
.laptop-section .text-column {
	display: flex;
	flex-direction: column;
	gap: 3.5rem;
	height: 100%;
	max-width: 500px;
	margin-top: 3rem;
}

.laptop-section .text-column {
	margin-top: 8rem;
}
.editor-section .text-segment h3,
.laptop-section .text-segment h3 {
	color: var(--very-dark-blue);
	font-size: clamp(1.2rem, 5vw, 1.6rem);
	font-weight: 500;
}

.editor-section .text-segment p,
.laptop-section .text-segment p {
	margin-top: 1rem;
	font-size: clamp(0.8rem, 2vw, 1rem);
	color: var(--dark-blue);
	line-height: 2rem;
	font-weight: 400;
}
.editor-section .img-column,
.laptop-section .img-column {
	min-height: 70vh;
	width: 100%;
}
.editor-img,
.laptop-img {
	position: absolute;
	top: 0px;
	right: clamp(-380px, -30vw, -800px);
	min-width: 700px;
}

.laptop-img {
	left: clamp(-380px, -30vw, -800px);
}
.phones-section {
	background: url("@/assets/bg-pattern-circles.svg"), var(--blue-bg);
	background-position: -5% 100%;
	background-repeat: no-repeat;
	margin-top: 10rem;
	border-radius: 0 100px 0 100px;
}

.phones-section-wrapper {
	width: 85%;
	margin: 0 auto;
	position: relative;
	min-height: 45vh;
}

.phones-section .equal-columns {
	display: flex;
	justify-content: space-between;
	align-items: center;
	width: 100%;
	gap: 3rem;
}

.phones-section .text-column {
	width: 50%;
}

.phones-section .img-column {
	min-height: 45vh;
	flex-basis: 50%;

	flex-shrink: 0;
}
.phones-img {
	position: absolute;
	top: -10%;
	left: 0;
	width: clamp(450px, 30vw, 800px);
}

.phones-section .text-column h2 {
	font-weight: 500;
	font-size: clamp(1.2rem, 10vw, 2rem);
	color: var(--white);
}

.phones-section .text-column p {
	margin-top: 1rem;
	font-size: clamp(0.8rem, 2vw, 1rem);
	color: var(--grayish-blue);
	line-height: 2rem;
	font-weight: 400;
}
@media (max-width: 1200px) {
	.phones-section-wrapper,
	.editor-section-wrapper {
		width: 100%;
	}
}
</style>
