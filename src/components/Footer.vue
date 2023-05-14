<script>
export default {};
</script>
<template>
	<!-- Product

Overview
Pricing
Marketplace
Features
Integrations

Company

About
Team
Blog
Careers

Connect

Contact
Newsletter
LinkedIn -->

	<footer>
		<div class="container">
			<div class="footer-wrapper">
				<div class="column"><img src="../assets/logo.svg" alt="Blogr logo" /></div>
				<div class="column">
					<h3>Product</h3>
					<ul>
						<li><a href="#">Overview</a></li>
						<li><a href="#">Pricing</a></li>
						<li><a href="#">Marketplace</a></li>
						<li><a href="#">Features</a></li>
						<li><a href="#">Integrations</a></li>
					</ul>
				</div>
				<div class="column">
					<h3>Company</h3>
					<ul>
						<li><a href="#">About</a></li>
						<li><a href="#">Team</a></li>
						<li><a href="#">Blog</a></li>
						<li><a href="#">Careers</a></li>
					</ul>
				</div>
				<div class="column">
					<h3>Connect</h3>
					<ul>
						<li><a href="#">Contact</a></li>
						<li><a href="#">Newsletter</a></li>
						<li><a href="#">LinkedIn</a></li>
					</ul>
				</div>
			</div>
		</div>
	</footer>
</template>
<style scoped>
footer {
	background: var(--dark-blue-bg);
	padding-block: 5rem;
	border-radius: 0 80px 0 0;
	color: var(--white);
}

.footer-wrapper {
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	align-items: start;
}
.column:first-child {
	margin-top: -1rem;
}
.column h3 {
	font-weight: 400;
	font-size: 1rem;
}

.column li a {
	font-size: 0.8rem;
	color: var(--grayish-blue);
	text-decoration: none;
}

.column li a:hover {
	text-decoration: underline 2px;
}

.column ul {
	margin-top: 2rem;
	display: flex;
	flex-direction: column;
	gap: 1rem;
}
</style>
