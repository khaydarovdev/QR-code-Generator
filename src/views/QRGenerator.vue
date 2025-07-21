<template>
	<div>
		<input type="text" placeholder="Generate" v-model="QRValue" />
		<!-- <qrcode-vue v-if="QRValue" :value="QRValue" size="250" level="H" id="vl" /> -->
		<qrcode-vue v-if="QRValue" :value="QRValue" :size="QRSize" level="H" id="vl" />
	</div>
</template>
<script>
import QrcodeVue from 'qrcode.vue';
export default {
	data() {
		return {
			QRValue: null,
			QRSize: window.innerWidth <= 640 ? 200 : 250,
		};
	},
	components: {
		QrcodeVue,
	},
	mounted() {
		window.addEventListener('resize', this.handleResize);
		this.handleResize(); // ensure correct size on mount
	},
	beforeDestroy() {
		window.removeEventListener('resize', this.handleResize);
	},
	methods: {
		handleResize() {
			this.QRSize = window.innerWidth <= 640 ? 200 : 250;
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
}
input {
	width: 450px;
	height: 30px;
	margin: 120px;
	border: none;
	background-color: white;
	border-radius: 15px;
	box-shadow: -15px -15px 15px rgba(255, 255, 255, 0.2), 15px 15px 15px rgba(0, 0, 0, 0.1),
		inset -50px -50px 50px rgba(255, 255, 255, 0.2), inset 50px 50px 50px rgba(0, 0, 0, 0.1);
	padding: 10px;
}
#vl {
	user-select: none;
}

@media (max-width: 640px) {
	input {
		width: 90%;
		margin: 60px 0;
		font-size: 16px;
		/* or simplified shadow for cleaner mobile look */
	}
	div {
		justify-content: flex-start;
		padding-top: 100px;
	}
}
</style>
