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
			showDropdown: false,
			selectedMenu: "",
		};
	},
	methods: {
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
	},

	watch: {
		selectedMenu(selected) {
			console.log(selected);
		},
	},
	mounted() {
		document.addEventListener("click", this.closeDropdown);
	},
	beforeUnmount() {
		document.removeEventListener("click", this.closeDropdown);
	},
};
</script>

<template>
	<nav>
		<div class="container">
			<img src="../assets/logo.svg" alt="" />
			<ul>
				<li ref="navItem">
					<a href="#" class="primary-link" @click="handleMenuClick('product')"
						>Product</a
					><SvgComp name="icon-arrow-light" :class="addRotationClass('product')" />
				</li>
				<li ref="navItem">
					<a href="#" class="primary-link" @click="handleMenuClick('company')"
						>Company</a
					><SvgComp name="icon-arrow-light" :class="addRotationClass('company')" />
				</li>
				<li ref="navItem">
					<div class="link-arrow" @click="handleMenuClick('connect')">
						<a href="#" class="primary-link">Connect</a
						><SvgComp
							name="icon-arrow-light"
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
						<a href="#" class="dropdown-link">Contact</a
						><a href="#" class="dropdown-link">Newsletter</a
						><a href="#" class="dropdown-link">Linkedin</a>
					</div>
				</li>
			</ul>
			<div class="auth-btns">
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

.container ul {
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
</style>
