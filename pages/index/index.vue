<template>
	<view class="content">
		<view class="phone-title">默认样式：</view>
		<phone-code ref="phoneCodeRef" @input-completed="handleInputCompleted" @input-change="handleInputChange">
		</phone-code>
		<view class="phone-title">全边框样式：</view>
		<phone-code :borderType="2">
		</phone-code>
		<view class="phone-title">全边框样式(定义边框/文本样式)：</view>
		<phone-code borderDefaultColor="#000000" borderFocusColor="#70DB93" inputType="text" :borderType="2">
		</phone-code>
		<view class="phone-title">无边框样式：</view>
		<phone-code :borderType="3">
		</phone-code>
	</view>
</template>

<script>
	import phoneCode from '@/components/phone-code/phone-code.vue'
	export default {
		components: {
			phoneCode
		},
		data() {
			return {
				verificationCode: '' // 验证码
			}
		},
		methods: {
			// 验证码输入完成回调
			handleInputCompleted(val) {
				this.verificationCode = val
				console.log('handleInputCompleted:', this.verificationCode)
			},
			//验证码输入未完成回调
			handleInputChange(val) {
				this.verificationCode = val
				console.log('handleInputChange:', this.verificationCode)
			}
		}
	}
</script>

<style scoped>
	.content {
		display: flex;
		flex-direction: column;
		padding: 10%;
	}

	.phone-title {
		margin-top: 60rpx;
		margin-bottom: 20rpx;
	}
</style>