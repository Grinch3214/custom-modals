<template>
	<Modal title="Modal with form" @close="$emit('close')">
		<template v-slot:body>
			<form @submit.prevent="sendSecondForm">
				<div class="input-group">
					<label class="input-group__label">Name</label>
					<input class="input-group__input" type="text"  required>
				</div>
				<div class="input-group">
					<label class="input-group__label">Email</label>
					<input class="input-group__input" type="email"  required>
				</div>
				<button class="btn btn--secondary">Send form</button>
			</form>
		</template>
	</Modal>
</template>

<script setup>
import Modal from './Modal.vue'
const emits = defineEmits(['close'])
</script>