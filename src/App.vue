<template>
  <div>
		<Modal v-if="modalFirst" title="Some title" />
	</div>
</template>

<script setup>
import Modal from './components/Modal.vue';
import { ref } from 'vue';

const modalFirst = ref(true)
</script>
