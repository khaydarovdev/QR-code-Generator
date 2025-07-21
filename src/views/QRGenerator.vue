<template>
	<div>
		<input type="text" placeholder="Generate" v-model="QRValue" />
		<qrcode-vue
			:style="{ opacity: QRValue ? 1 : 0 }"
			:value="QRValue"
			size="250"
			level="H"
			id="vl"
		/>
	</div>
</template>

<script>
import QrcodeVue from 'qrcode.vue';

export default {
	data() {
		return {
			QRValue: null,
		};
	},
	components: {
		QrcodeVue,
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
	position: relative;
}

/* Input styling */
input {
	width: 450px;
	height: 30px;
	border: none;
	background-color: white;
	border-radius: 15px;
	box-shadow: -15px -15px 15px rgba(255, 255, 255, 0.2), 15px 15px 15px rgba(0, 0, 0, 0.1),
		inset -50px -50px 50px rgba(255, 255, 255, 0.2), inset 50px 50px 50px rgba(0, 0, 0, 0.1);
	padding: 10px;
	margin-bottom: 40px;
	transition: all 0.3s ease;
}

/* QR code placeholder */
#vl,
qrcode-vue {
	width: 250px;
	height: 250px;
	user-select: none;
	display: block;
	transition: opacity 0.3s ease;
}

/* Mobile Responsive */
@media (max-width: 768px) {
	input {
		width: 80%;
		box-shadow: -10px -10px 10px rgba(255, 255, 255, 0.2), 10px 10px 10px rgba(0, 0, 0, 0.1),
			inset -20px -20px 20px rgba(255, 255, 255, 0.2), inset 20px 20px 20px rgba(0, 0, 0, 0.1);
	}

	#vl,
	qrcode-vue {
		width: 200px;
		height: 200px;
	}
}
</style>
