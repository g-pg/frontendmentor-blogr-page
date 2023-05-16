<script>
import SvgComp from "./SvgComp.vue";
import PrimaryBtn from "./PrimaryBtn.vue";
export default {
	components: {
		SvgComp,
		PrimaryBtn,
	},

	data() {
		return {
			burgerOpen: false,
			showDropdown: false,
			selectedMenu: "",
			windowWidth: window.innerWidth,
		};
	},
	methods: {
		toggleBurger() {
			this.burgerOpen = !this.burgerOpen;
		},
		addRotationClass(menu) {
			if (this.showDropdown && this.selectedMenu === menu) {
				return "rotated-arrow";
			}
			return "";
		},

		handleMenuClick(menu) {
			if (this.selectedMenu === menu) {
				this.showDropdown = false;
				return (this.selectedMenu = "");
			}

			(this.showDropdown = true), (this.selectedMenu = menu);
		},
		closeDropdown(e) {
			const navUlRef = this.$refs.navRef;
			if (navUlRef && !navUlRef.contains(e.target)) {
				this.showDropdown = false;
				return (this.selectedMenu = "");
			}
		},
		closeBurger(e) {
			const navRef = this.$refs.navRef;
			const burgerBtnRef = this.$refs.burgerBtnRef;

			if (
				navRef &&
				burgerBtnRef &&
				!navRef.contains(e.target) &&
				!burgerBtnRef.contains(e.target)
			) {
				this.burgerOpen = false;
			}
		},
		updateWindowWidth() {
			this.windowWidth = window.innerWidth;
		},
	},

	mounted() {
		document.addEventListener("click", this.closeDropdown);
		document.addEventListener("click", this.closeBurger);
		window.addEventListener("resize", this.updateWindowWidth);
	},
	beforeUnmount() {
		document.removeEventListener("click", this.closeDropdown);
		document.removeEventListener("click", this.closeBurger);
		window.removeEventListener("resize", this.updateWindowWidth);
	},
	computed: {
		burgerIconPath() {
			return this.burgerOpen ? "/icon-close.svg" : "./icon-hamburger.svg";
		},
		arrowIcon() {
			return this.isMobile ? "icon-arrow-dark" : "icon-arrow-light";
		},
		isMobile() {
			return this.windowWidth <= 980;
		},
	},

	watch: {
		burgerOpen(isOpen) {
			if (isOpen) {
				document.body.style.overflow = "hidden";
			} else {
				document.body.style.overflow = "unset";
			}
		},
	},
};
</script>

<template>
	<nav>
		<div class="container">
			<a href="#"><img src="/logo.svg" alt="Blogr logo" /></a>
			<button @click="toggleBurger" class="burger-btn" ref="burgerBtnRef">
				<img :src="burgerIconPath" alt="" />
			</button>
			<div v-if="!isMobile || burgerOpen" class="nav-wrapper" ref="navRef">
				<ul :class="['main-nav-ul', isMobile ? 'mobile' : '']" ref="navUlRef">
					<li class="navItem">
						<div class="link-arrow" @click="handleMenuClick('product')">
							<a href="#" class="primary-link">Product</a
							><SvgComp
								:name="arrowIcon"
								:class="addRotationClass('product')"
							/>
						</div>
						<div
							class="dropdown"
							:class="{
								show: this.showDropdown && this.selectedMenu === 'product',
							}"
							ref="dropdownRef"
						>
							<a href="#">Overview</a>
							<a href="#">Pricing</a>
							<a href="#">Marketplace</a>
							<a href="#">Features</a>
							<a href="#">Integrations</a>
						</div>
					</li>
					<li class="navItem">
						<div class="link-arrow" @click="handleMenuClick('Company')">
							<a href="#" class="primary-link">Company</a
							><SvgComp
								:name="arrowIcon"
								:class="addRotationClass('company')"
							/>
						</div>
						<div
							class="dropdown"
							:class="{
								show: this.showDropdown && this.selectedMenu === 'Company',
							}"
							ref="dropdownRef"
						>
							<a href="#">About</a><a href="#">Team</a><a href="#">Blog</a
							><a href="#">Careers</a>
						</div>
					</li>
					<li class="navItem">
						<div class="link-arrow" @click="handleMenuClick('connect')">
							<a href="#" class="primary-link">Connect</a
							><SvgComp
								:name="arrowIcon"
								:class="addRotationClass('connect')"
							/>
						</div>
						<div
							class="dropdown"
							:class="{
								show: this.showDropdown && this.selectedMenu === 'connect',
							}"
							ref="dropdownRef"
						>
							<a href="#">Contact</a><a href="#">Newsletter</a
							><a href="#">Linkedin</a>
						</div>
					</li>
				</ul>
				<div v-if="!isMobile || burgerOpen" class="auth-btns">
					<a href="#" class="primary-link">Login</a>
					<a href="#">
						<PrimaryBtn
							content="Sign Up"
							filled
							padding
							:red="isMobile ? true : false"
						/>
					</a>
				</div>
			</div>
		</div>
	</nav>
</template>

<style scoped>
.container {
	display: flex;
	align-items: center;
	gap: 3rem;
	margin-top: 0.5rem;
}

.nav-wrapper {
	display: flex;
	align-items: center;
	justify-content: space-between;
	gap: 1rem;
	width: 100%;
}
.main-nav-ul {
	display: flex;
	gap: 2rem;
	align-items: center;
}

.container li {
	cursor: pointer;
	position: relative;
}
.container li svg {
	margin-left: 0.5rem;
	cursor: pointer;
}
a {
	text-decoration: none;
	color: var(--white);
	cursor: pointer;
}
.primary-link {
	font-weight: 500;
}

.primary-link:hover {
	text-decoration: underline 2px;
}

.link-arrow > * {
	transition: 0.3s ease;
}
.rotated-arrow {
	transform: rotate(180deg);
}

.dropdown {
	position: absolute;
	background: var(--white);
	display: flex;
	flex-direction: column;
	gap: 0.8rem;
	padding: 1.7rem 1.3rem;
	border-radius: 6px;
	min-width: 150px;
	top: 40px;
	left: -20px;
	box-shadow: 2px 3px 15px 3px rgb(0, 0, 0, 0.3);
	/* animation: roll 0.3s ease-in forwards; */
	transition: 0.3s ease-in;
	display: none;
	z-index: 10;
}

.show {
	display: flex;
	cursor: pointer;
	animation: roll 0.3s ease-out forwards;
	transition: 0.5s ease;
}

@keyframes roll {
	0% {
		opacity: 0;
		transform: translateY(-20px);
	}

	100% {
		opacity: 1;
		transform: translateY(0);
	}
}

.dropdown a {
	color: var(--black);
	font-size: 0.9rem;
	font-weight: 500;
}
.dropdown a:hover {
	font-weight: 700;
}
.auth-btns {
	margin-left: auto;
	display: flex;
	align-items: center;
	gap: 1.5rem;
}

.burger-btn {
	display: none;
}
@media (max-width: 980px) {
	.container {
		position: relative;
	}

	.nav-wrapper {
		width: unset;
		position: absolute;
		z-index: 999;
		width: 90%;
		height: 80vh;
		inset: 0;
		margin: 0 auto;
		transform: translateY(70px);
		background: var(--white);
		flex-direction: column;
		align-items: center;
		gap: 2.5rem;
		padding: 3rem 2rem;
		box-shadow: 0px 5px 15px 3px rgb(0, 0, 0, 0.2);
		border-radius: 8px;
	}
	.burger-btn {
		display: unset;
		margin-left: auto;
		background: none;
		border: none;
		cursor: pointer;
	}
	.auth-btns {
		margin: 0 auto;
		flex-direction: column;
		border-top: 1px solid var(--grayish-blue);
		width: 100%;
		padding-top: 3rem;
	}
	.main-nav-ul {
		display: flex;
		flex-direction: column;
		align-items: center;
		width: 100%;
	}

	.primary-link {
		color: var(--very-dark-blue);
		font-size: 1.2rem;
	}
	.container li {
		width: 100%;
		margin: 0 auto;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
	}
	.dropdown {
		text-align: center;
		background: #d0d0d3;
		box-shadow: none;
		width: 100%;
		left: 0;
		margin: 0 auto;
		gap: 1.8rem;
		position: relative;
		top: 10px;
		/* animation: roll 0.3s ease-in forwards; */
	}
	.dropdown a {
		color: var(--very-dark-blue);
		font-size: 1.1rem;
	}
}
</style>
