<template>
  <div class="container">
		<div class="m">
			<button class="btn btn--primary" @click="modalFirst = true">Open modal</button>
			<Modal v-show="modalFirst" title="Some title" @close="modalFirst = false">
				<template v-slot:body>
					<div>
						Lorem ipsum dolor sit amet consectetur adipisicing elit. Sequi, et necessitatibus. Accusamus, earum sed non praesentium itaque dolore? Esse perferendis distinctio eos vitae deleniti ab, ad ea nemo enim dicta.
					</div>
				</template>
			</Modal>

			<button class="btn btn--primary" @click="modalSecond.show = true">Open modal with form</button>
			<Modal v-show="modalSecond.show" title="Modal with form" @close="modalSecond.show = false">
				<template v-slot:body>
					<form @submit.prevent="sendSecondForm">
						<div class="input-group">
							<label class="input-group__label">Name</label>
							<input class="input-group__input" type="text" v-model="modalSecond.name" required>
						</div>
						<div class="input-group">
							<label class="input-group__label">Email</label>
							<input class="input-group__input" type="email" v-model="modalSecond.email" required>
						</div>
						<button class="btn btn--secondary">Send form</button>
					</form>
				</template>
			</Modal>
			
			<button class="btn btn--primary" @click="modalValidate = true">Open modal with validate</button>
			<ModalValidate v-show="modalValidate" @close="modalValidate">

			</ModalValidate>

		</div>
	</div>
</template>

<script setup>
import Modal from './components/Modal.vue'
import ModalValidate from './components/ModalValidate.vue'
import { ref } from 'vue'

const modalFirst = ref(false)
const modalValidate = ref(false)
const modalSecond = ref({
	show: false,
	name: '',
	email: ''
})

const sendSecondForm = () => {
	console.log({
		name: modalSecond.value.name,
		email: modalSecond.value.email
	})
	modalSecond.value.name = ''
	modalSecond.value.email = ''
	modalSecond.value.show = false
}

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
