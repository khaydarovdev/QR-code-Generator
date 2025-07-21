<template>
	<div :class="['container', { 'moved-up': QRValue }]">
		<input type="text" placeholder="Generate" v-model="QRValue" />
		<transition name="fade">
			<qrcode-vue v-if="QRValue" :value="QRValue" :size="qrSize" level="H" id="vl" />
		</transition>
	</div>
</template>

<script>
import QrcodeVue from 'qrcode.vue';

export default {
	data() {
		return {
			QRValue: '',
			qrSize: 250,
		};
	},
	components: {
		QrcodeVue,
	},
	mounted() {
		this.setQRSize();
		window.addEventListener('resize', this.setQRSize);
	},
	beforeDestroy() {
		window.removeEventListener('resize', this.setQRSize);
	},
	methods: {
		setQRSize() {
			// Set smaller QR size on small screens
			this.qrSize = window.innerWidth <= 768 ? 200 : 250;
		},
	},
};
</script>

<style scoped>
/* Desktop default */
.container {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	min-height: 100vh;
	padding: 0 20px;
	transition: all 0.5s ease;
}

.container.moved-up {
	justify-content: flex-start;
	padding-top: 100px;
}

input {
	width: 450px;
	height: 40px;
	border: none;
	background-color: white;
	border-radius: 15px;
	box-shadow: -15px -15px 15px rgba(255, 255, 255, 0.2), 15px 15px 15px rgba(0, 0, 0, 0.1),
		inset -50px -50px 50px rgba(255, 255, 255, 0.2), inset 50px 50px 50px rgba(0, 0, 0, 0.1);
	padding: 10px 20px;
	font-size: 18px;
	transition: all 0.5s ease;
	margin-top: 40px;
}

#vl {
	user-select: none;
	margin-top: 30px;
}

/* Smooth fade for QR */
.fade-enter-active,
.fade-leave-active {
	transition: opacity 0.5s ease;
}
.fade-enter-from,
.fade-leave-to {
	opacity: 0;
}

/* 📱 Mobile Media Query */
@media (max-width: 768px) {
	.container.moved-up {
		padding-top: 60px;
	}

	input {
		width: 90%;
		font-size: 16px;
		height: 35px;
		box-shadow: -8px -8px 10px rgba(255, 255, 255, 0.2), 8px 8px 10px rgba(0, 0, 0, 0.1),
			inset -30px -30px 30px rgba(255, 255, 255, 0.2), inset 30px 30px 30px rgba(0, 0, 0, 0.1);
	}

	#vl {
		margin-top: 20px;
	}
}
</style>
