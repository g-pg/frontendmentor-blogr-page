<script setup>
import { defineAsyncComponent } from "vue";

const props = defineProps({
	name: {
		type: String,
		required: true,
	},
});

const SvgComp = defineAsyncComponent(() => import(`../assets/${props.name}.svg`));
</script>

<template>
	<component :is="SvgComp" class="fill-current" />
</template>
