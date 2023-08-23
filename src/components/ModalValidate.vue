<template>
	<Modal title="Modal with form" @close="$emit('close')">
		<template v-slot:body>
			<form @submit.prevent="sendSecondForm">
				<div class="input-group">
					<label class="input-group__label">Name</label>
					<input
					  v-model="formData.name"
						@change="v$.name.$touch()"
					  :class="{ 'input-group__input--error': v$.name.$error }"
					  class="input-group__input"
					  type="text"
					>
					<p class="input-group__error" v-if="v$.name.$error">This field should be at least 2 characters long</p>
				</div>
				<div class="input-group last-child">
					<label class="input-group__label">Email</label>
					<input
					  v-model="formData.email"
						@change="v$.email.$touch()"
					  :class="{ 'input-group__input--error': v$.email.$error }"
					  class="input-group__input"
					  type="text"
					>
					<p v-if="v$.email.$error" class="input-group__error">Value is not a valid email address</p>
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
	}),
	v$.value.$reset()
	} else {
		console.log('Not Valid')
	}
}
</script>