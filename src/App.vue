<template>
  <div class="container">
		<div class="m">
			<button class="btn btn--primary" @click="modalFirst = !modalFirst">Open modal</button>
			<Modal v-if="modalFirst" title="Some title" />
		</div>
	</div>
</template>

<script setup>
import Modal from './components/Modal.vue';
import { ref } from 'vue';

const modalFirst = ref(false)
</script>

<style lang="scss" scoped>
	.m {
		margin-top: 25px;
	}
</style>
