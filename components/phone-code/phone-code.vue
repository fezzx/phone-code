<template>
	<view class="code-container">
		<!-- 数字显示区域 -->
		<view class="digits">
			<view class="digit" :class="[{ 'digit--focus': isInputFocused && index === inputArray.length }, 
                  { 'digit--border-all': borderType === 2 }, 
                  { 'digit--no-border': borderType === 3 }]"
				:style="{ 'border-color': isInputFocused && index === inputArray.length ? borderFocusColor : borderDefaultColor }"
				v-for="(item, index) in digitArray" :key="index">
				{{inputArray[item] || ''}}
			</view>
		</view>
		<!-- 隐藏的实际输入框 -->
		<input class="digit-input" :maxlength="digitLength" v-model="inputValue" :focus="isInputFocused"
			@input="handleInput" @focus="handleFocus" @blur="handleBlur" :type="inputType" />
	</view>
</template>

<script>
	export default {
		name: "PhoneCode",
		props: {
			// 边框类型：1-下边框，2-全边框，3-无边框
			borderType: {
				type: Number,
				default: 1
			},
			// 默认边框颜色
			borderDefaultColor: {
				type: String,
				default: '#aaaaaa'
			},
			// 聚焦时边框颜色
			borderFocusColor: {
				type: String,
				default: '#2f6df5'
			},
			// 验证码位数
			digitLength: {
				type: Number,
				default: 6
			},
			// 输入类型（number/text等）
			inputType: {
				type: String,
				default: 'number'
			},
		},
		data() {
			return {
				digitArray: [], // 数字框索引数组
				inputValue: '', // 输入框的值，比如:123456
				inputArray: [], // 转为验证码数组，比如:[1, 2, 3, 4, 5, 6]
				isInputFocused: false, // 是否获得焦点
			}
		},
		watch: {
			digitLength(newVal, oldVal) {
				this.initDigitArray()
			}
		},
		created() {
			this.initDigitArray()
			this.handleFocus()
		},
		methods: {
			// 初始化数字框
			initDigitArray() {
				const len = this.digitLength
				const tempArray = []
				for (let i = 0; i < len; i++) {
					tempArray.push(i)
				}
				this.digitArray = tempArray
			},
			// 处理输入事件
			handleInput(e) {
				const inputValue = e.detail.value
				this.inputArray = inputValue.split('')
				// 当输入长度等于要求长度时触发完成事件
				if (this.inputArray.length === this.digitLength) {
					this.$emit('input-completed', inputValue)
				} else {
					// 输入未完成时触发一个事件
					this.$emit('input-change', inputValue)
				}
			},
			// 处理聚焦事件
			handleFocus(e) {
				this.isInputFocused = true
			},
			// 处理失焦事件
			handleBlur(e) {
				this.isInputFocused = false
			},
		},
	};
</script>

<style scoped>
	/* 主容器 */
	.code-container {
		height: 80rpx;
		position: relative;
		overflow: hidden;
	}

	/* 数字框容器 */
	.code-container .digits {
		display: flex;
	}

	/* 单个数字框基础样式 */
	.code-container .digit {
		position: relative;
		flex: 1;
		border-bottom: 1px solid;
		margin: 0 5px;
		text-align: center;
		line-height: 75rpx;
		height: 75rpx;
	}

	/* 全边框样式 */
	.code-container .digit--border-all {
		border: 1px solid;
		border-radius: 12rpx;
	}

	/* 无边框样式 */
	.code-container .digit--no-border {
		border: 0;
	}

	/* 聚焦时的闪烁光标 */
	.code-container .digit--focus::before {
		position: absolute;
		left: 50%;
		content: '';
		background: #aaa;
		width: 1px;
		height: 50%;
		top: 25%;
		animation: cursor-blink 1s linear infinite;
	}

	/* 光标闪烁动画 */
	@keyframes cursor-blink {

		0%,
		100% {
			opacity: 1;
		}

		50% {
			opacity: 0;
		}
	}

	/* 隐藏的输入框 */
	.code-container .digit-input {
		opacity: 0;
		position: absolute;
		top: 0;
		left: -100%;
		width: 200%;
		height: 75rpx;
	}

	/* 首数字框边距调整 */
	.code-container .digit-input:first-child {
		margin-left: 0;
	}

	/* 尾数字框边距调整 */
	.code-container .digit-input:last-child {
		margin-right: 0;
	}
</style>