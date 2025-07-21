<template>
	<div class="container">
		<div class="content" :class="{ 'moved-up': QRValue }">
			<input type="text" placeholder="Generate" v-model="QRValue" />
			<transition name="fade">
				<qrcode-vue v-if="QRValue" :value="QRValue" size="250" level="H" id="vl" />
			</transition>
		</div>
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
.container {
	height: 100vh;
	display: flex;
	align-items: center;
	justify-content: center;
}

.content {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	transition: transform 0.4s ease-in-out;
}

.content.moved-up {
	transform: translateY(-100px);
}

input {
	width: 450px;
	height: 30px;
	margin: 30px;
	border: none;
	background-color: white;
	border-radius: 15px;
	box-shadow: -15px -15px 15px rgba(255, 255, 255, 0.2), 15px 15px 15px rgba(0, 0, 0, 0.1),
		inset -50px -50px 50px rgba(255, 255, 255, 0.2), inset 50px 50px 50px rgba(0, 0, 0, 0.1);
	padding: 10px;
}

#vl {
	user-select: none;
	margin-top: 20px;
}

/* Optional fade animation for the QR */
.fade-enter-active,
.fade-leave-active {
	transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
	opacity: 0;
}
</style>
