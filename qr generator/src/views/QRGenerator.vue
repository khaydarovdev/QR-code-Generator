<template>
	<div>
		<input type="text" placeholder="Generate" v-model="QRValue" />
		<div class="qr">
			<qrcode-vue v-if="QRValue" :value="QRValue" size="250" level="H" id="vl" />
		</div>
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
input {
	width: 450px;
	height: 50px;
	margin: 150px 550px;
	border: none;
	background-color: white;
	border-radius: 15px;
	box-shadow: -15px -15px 15px rgba(255, 255, 255, 0.2), 15px 15px 15px rgba(0, 0, 0, 0.1),
		inset -50px -50px 50px rgba(255, 255, 255, 0.2), inset 50px 50px 50px rgba(0, 0, 0, 0.1);
	padding: 10px;
}
.qr {
	width: max-content;
	height: max-content;
	margin-left: 670px;
	box-shadow: -25px -25px 25px rgba(255, 255, 255, 0.2), 55px 55px 55px rgba(0, 0, 0, 0.1),
		inset -60px -60px 60px rgba(255, 255, 255, 0.2), inset 100px 100px 100px rgba(0, 0, 0, 0.1);
}
</style>
