<template>
	<Modal title="Modal with form" @close="$emit('close')">
		<template v-slot:body>
			<form @submit.prevent="sendSecondForm">
				<div class="input-group">
					<label class="input-group__label">Name</label>
					<input class="input-group__input" type="text" v-model="formData.name">
				</div>
				<div class="input-group">
					<label class="input-group__label">Email</label>
					<input class="input-group__input" type="text" v-model="formData.email">
				</div>
				<button class="btn btn--secondary">Send form</button>
			</form>
		</template>
	</Modal>
</template>

<script setup>
import { ref, computed } from 'vue'
import { useVuelidate } from '@vuelidate/core'
import { required, email, minLength } from '@vuelidate/validators'
import Modal from './Modal.vue'
const emits = defineEmits(['close'])

// Validate
const formData = ref({
	name: '',
	email: ''
})

const rules = computed(() => {
	return {
		name: { required, minLength: minLength(2) },
		email: { required, email }
	}
})

const v$ = useVuelidate(rules, formData)

const sendSecondForm = () => {
	v$.value.$validate()
	console.log(v$.value.$error)
	if(!v$.value.$error) {
		console.log('Valid')
		console.log({
		name: formData.value.name,
		email: formData.value.email
	})
	} else {
		console.log('Not Valid')
	}
}
</script>