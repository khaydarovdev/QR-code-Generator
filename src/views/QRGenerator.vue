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
div {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	min-height: 100vh;
	padding: 20px;
	box-sizing: border-box;
	transition: all 0.3s ease;
}

input {
	width: 450px;
	height: 30px;
	border: none;
	background-color: white;
	border-radius: 15px;
	box-shadow:
		-15px -15px 15px rgba(255, 255, 255, 0.2),
		15px 15px 15px rgba(0, 0, 0, 0.1),
		inset -50px -50px 50px rgba(255, 255, 255, 0.2),
		inset 50px 50px 50px rgba(0, 0, 0, 0.1);
	padding: 10px;
	transition: all 0.3s ease;
}

#vl {
	margin-top: 40px;
	user-select: none;
	transition: all 0.3s ease;
}

/* 📱 Responsive for mobile */
@media (max-width: 768px) {
	input {
		width: 80%;
		margin: 0;
		margin-bottom: 20px;
		box-shadow:
			-10px -10px 10px rgba(255, 255, 255, 0.2),
			10px 10px 10px rgba(0, 0, 0, 0.1),
			inset -20px -20px 20px rgba(255, 255, 255, 0.2),
			inset 20px 20px 20px rgba(0, 0, 0, 0.1);
	}
}
</style>
