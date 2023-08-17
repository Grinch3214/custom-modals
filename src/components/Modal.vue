<template>
	<Transition name="modal-animation" appear>
		<div class="modal" @click="$emit('close')">
      <div class="modal__content" @click.stop>

        <div class="modal__header">
          <span class="modal__title"> {{ title }} </span>
          <span class="modal__close" @click="$emit('close')"></span>
        </div>

        <div class="modal__body">
					<slot name="body"></slot>
				</div>
      </div>
    </div>
	</Transition>
</template>

<script setup>
import { onMounted } from 'vue'
const emits = defineEmits(['close'])
const props = defineProps({
	title: {
		type: String,
		required: true
	}
})
onMounted(() => {
  document.body.addEventListener('keyup', e => {
		if(e.key === 'Escape') {
			emits('close')
		}
	})
})
</script>

<style>
.modal-animation-enter-active, .modal-animation-leave-active {
	opacity: 0;
}
.modal-animation-enter-active .modal__content,
.modal-animation-leave-active .modal__content {
	transform: scale(.5);
}
</style>


<style lang="scss" scoped>

.modal {
	display: flex;
	justify-content: center;
	align-items: center;
	position: fixed;
	top: 0;
	bottom: 0;
	left: 0;
	transition: opacity .2s ease;
	right: 0;
	z-index: 998;
	background-color: rgba(0,0,0,.48);

	&__content {
		position: relative;
		max-width: 600px;
		padding: 20px 18px;
		background-color: #fff;
		border: 1px solid #dcdfe6;
		transition: all .2s ease;
		border-radius: 8px;
		z-index: 999;
		overflow: hidden;
		@media screen and (min-width: 900px) {
			min-width: 500px;
		}
	}

	&__header {
		display: flex;
		align-self: center;
		justify-content: space-between;
		padding-bottom: 20px;
		span {
			font-size: 24px;
		}
	}

	&__title {
		font-weight: 600;
	}

	&__close {
		cursor: pointer;
		position: relative;
		width: 20px;
		height: 20px;

		&::before, &::after {
			content: '';
			position: absolute;
			top: 50%;
			left: 0;
			right: 0;
			background: #000;
			height: 2px;
			transform: rotate(45deg);
		}

		&::after {
			transform: rotate(-45deg);
		}
	}

	&__body {
		text-align: center;
	}
}
</style>
