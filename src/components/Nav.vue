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
		closeDropdown(event) {
			if (!this.$refs.navItem.contains(event.target)) {
				this.showDropdown = false;
				this.selectedMenu = "";
			}
		},
		updateWindowWidth() {
			this.windowWidth = window.innerWidth;
		},
	},

	// watch: {
	// 	windowWidth(newWidth) {
	// 		console.log("newidth", newWidth);
	// 	},
	// },
	mounted() {
		document.addEventListener("click", this.closeDropdown);
		window.addEventListener("resize", this.updateWindowWidth);
	},
	beforeUnmount() {
		document.removeEventListener("click", this.closeDropdown);
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
			return this.windowWidth > 980 ? false : true;
		},
	},
};
</script>

<template>
	<nav>
		<div class="container">
			<img src="../assets/logo.svg" alt="Blogr logo" />
			<button @click="toggleBurger" class="burger-btn">
				<img :src="burgerIconPath" alt="" />
			</button>
			<ul
				v-if="!isMobile || burgerOpen"
				:class="['main-nav-ul', isMobile ? 'mobile' : '']"
			>
				<li ref="navItem">
					<a href="#" class="primary-link" @click="handleMenuClick('product')"
						>Product</a
					><SvgComp :name="arrowIcon" :class="addRotationClass('product')" />
				</li>
				<li ref="navItem">
					<a href="#" class="primary-link" @click="handleMenuClick('company')"
						>Company</a
					><SvgComp :name="arrowIcon" :class="addRotationClass('company')" />
				</li>
				<li ref="navItem">
					<div class="link-arrow" @click="handleMenuClick('connect')">
						<a href="#" class="primary-link">Connect</a
						><SvgComp :name="arrowIcon" :class="addRotationClass('connect')" />
					</div>

					<div
						class="dropdown"
						:class="{
							show: this.showDropdown && this.selectedMenu === 'connect',
						}"
						ref="dropdownRef"
					>
						<a href="#" class="dropdown-link">Contact</a
						><a href="#" class="dropdown-link">Newsletter</a
						><a href="#" class="dropdown-link">Linkedin</a>
					</div>
				</li>
			</ul>
			<div v-if="!isMobile || burgerOpen" class="auth-btns">
				<a href="#" class="primary-link">Login</a>
				<a href="#">
					<PrimaryBtn content="Sign Up" hollow padding />
				</a>
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

.dropdown-link {
	color: var(--black);
	font-size: 0.9rem;
	font-weight: 500;
}

.dropdown-link:hover {
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
	.burger-btn {
		display: unset;
		margin-left: auto;
		background: none;
		border: none;
		cursor: pointer;
	}
	.auth-btns {
		display: none;
	}
	.main-nav-ul {
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
		padding: 2.5rem;
		box-shadow: 0px 5px 15px 3px rgb(0, 0, 0, 0.2);
		border-radius: 8px;
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
	}
	.dropdown {
		text-align: center;
		background: #d0d0d3;
		box-shadow: none;
		width: 100%;
		left: 0;
		margin: 0 auto;
		gap: 1.8rem;
		/* animation: roll 0.3s ease-in forwards; */
	}

	.dropdown-link {
		color: var(--very-dark-blue);
		font-size: 1.1rem;
	}
}
</style>