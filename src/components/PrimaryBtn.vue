<script>
export default {
	props: {
		content: {
			type: String,
			required: true,
		},

		filled: {
			type: Boolean,
			required: false,
		},
		red: {
			type: String,
			required: false,
		},
		padding: {
			type: Boolean,
			required: false,
		},

		customStyle: {
			type: Object,
			required: false,
		},
	},
};
</script>

<template>
	<button
		:class="[filled ? 'filled' : 'hollow', padding ? 'padding' : '', red ? 'red' : '']"
		:style="customStyle"
	>
		{{ content }}
	</button>
</template>

<style scoped>
button {
	border: none;
	background: none;
	padding: 0.7rem 0.8rem;
	display: flex;
	justify-content: center;
	align-items: center;
	font-weight: 700;
	border-radius: 25px;
	width: max-content;
	cursor: pointer;
}

.padding {
	padding: 0.7rem 2rem;
}
.filled,
.hollow:hover {
	background: var(--white);
	color: var(--light-red);
}

.filled:hover {
	background: var(--very-light-red);
	color: var(--white);
}

.hollow {
	border: 1px solid var(--white);
	color: var(--white);
	font-weight: 500;
}

.red {
	background: var(--red-bg);
	color: var(--white);
}
.red:hover {
	background: var(--red-bg);
}
</style>
