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
		<section class="editor-section">
			<div class="container">
				<div class="section-wrapper editor">
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
								:src="
									isMobile
										? '/illustration-editor-mobile.svg'
										: '/illustration-editor-desktop.svg'
								"
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
				<div class="section-wrapper phones">
					<div class="equal-columns">
						<div class="img-column">
							<img
								src="../../assets/illustration-phones.svg"
								alt="Design sketch with scribbled lines, circles and squares"
								class="phones-img"
							/>
						</div>
						<div class="text-column">
							<div class="text-segment">
								<h2 class="section-title white">
									State of the Art Infrastructure
								</h2>
								<p>
									With reliability and speed in mind, worldwide data
									centers provide the backbone for ultra-fast
									connectivity. This ensures your site will load
									instantly, no matter where your readers are, keeping
									your site competitive.
								</p>
							</div>
						</div>
					</div>
				</div>
			</div>
		</section>
		<section class="laptop-section">
			<div class="container">
				<div class="section-wrapper laptop">
					<div class="equal-columns">
						<div class="img-column">
							<img
								:src="
									isMobile
										? '/illustration-laptop-mobile.svg'
										: '/illustration-laptop-desktop.svg'
								"
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
	</PageLayout>
</template>

<style scoped>
section {
	margin-block: 10rem;
}
.section-title {
	text-align: center;
	font-size: clamp(1.2rem, 10vw, 2rem);
	font-weight: 500;
}

.section-title.blue {
	color: var(--very-dark-blue);
}
.section-title.white {
	color: var(--white);
}

.section-wrapper {
	position: relative;
	width: 80%;
	margin: 0 auto;
	min-height: 90vh;
}

.equal-columns {
	display: flex;
	align-items: center;
	justify-content: space-between;
	gap: 5rem;
}

.equal-columns > div {
	margin-top: 8rem;
	flex-basis: 50%;
}

.text-column {
	display: flex;
	flex-direction: column;
	gap: 3.5rem;
	height: 100%;
	margin-top: 8rem;
}

.text-segment h3 {
	color: var(--very-dark-blue);
	font-size: clamp(1.7rem, 5vw, 1.8rem);
	font-weight: 500;
}
.text-segment p {
	margin-top: 1rem;
	font-size: clamp(1.1rem, 2vw, 1.1rem);
	font-size: 1.1rem;
	color: var(--dark-blue);
	line-height: 2rem;
	font-weight: 400;
}

.img-column {
	position: relative;
	align-self: stretch;
	flex-shrink: 0;
	display: grid;
	place-items: center;
}

.editor-img {
	position: absolute;
	transform: scale(1.7);
	min-width: 300px;
	right: -50%;
}

.laptop-img {
	position: absolute;
	transform: scale(1.7);
	min-width: 300px;
	left: -50%;
}

.phones-section {
	background: url("@/assets/bg-pattern-circles.svg"), var(--blue-bg);
	background-position: -5% 100%;
	background-repeat: no-repeat;
	border-radius: 0 100px 0 100px;
}

.section-wrapper.phones {
	min-height: unset;
	margin-block: 18rem;
	padding-block: 6rem;
}
.phones-section .section-title {
	text-align: left;
}
.phones-section p {
	color: var(--white);
	color: var(--grayish-blue);
}

.phones-section .equal-columns > div {
	margin-top: 0;
}
.phones-img {
	position: absolute;
}

@media (max-width: 980px) {
	section {
		margin-block: 5rem;
	}
	.section-wrapper {
		width: 100%;
		min-height: unset;
	}
	.equal-columns {
		flex-direction: column;
		gap: 2rem;
	}
	.editor .equal-columns {
		flex-direction: column-reverse;
	}
	.equal-columns > div {
		margin-top: 3rem;
	}

	.img-column {
		align-self: unset;
	}
	.editor-img,
	.laptop-img {
		position: unset;
		transform: unset;
	}

	.text-column {
		text-align: center;
	}

	.section-wrapper.phones {
		padding-top: 10rem;
		margin-bottom: 0;
	}
	.phones .img-column {
		align-self: stretch;
	}

	.phones-img {
		transform: translateY(-40%);
		max-width: 400px;
	}
	.phones .section-title {
		text-align: center;
	}
}
</style>
