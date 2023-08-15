<template>
  <div class="container">
		<div class="m">
			<button class="btn btn--primary" @click="modalFirst = !modalFirst">Open modal</button>
			<Modal v-if="modalFirst" title="Some title" @close="modalFirst = !modalFirst" />
		</div>
	</div>
</template>

<script setup>
import Modal from './components/Modal.vue';
import { ref } from 'vue';

const modalFirst = ref(false)
</script>

<style>
@font-face {
	font-family: 'Open Sans';
	src: url('./assets/fonts/OpenSans-Regular.woff2') format('woff2');
	font-weight: 400;
	font-style: normal;
	font-display: swap;
}

@font-face {
	font-family: 'Open Sans';
	src: url('./assets/fonts/OpenSans-SemiBold.woff2') format('woff2');
	font-weight: 600;
	font-style: normal;
	font-display: swap;
}

@font-face {
	font-family: 'Open Sans';
	src: url('./assets/fonts/OpenSans-ExtraBold.woff2') format('woff2');
	font-weight: 800;
	font-style: normal;
	font-display: swap;
}
</style>

<style lang="scss" scoped>
	.m {
		margin-top: 25px;
	}
</style>
