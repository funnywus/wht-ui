<template>
	<view class="demo-input">
		<view class="demo-section">
			<view class="demo-title">基础用法</view>
			<wht-input v-model="value1" placeholder="请输入文本" />
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义类型</view>
			<wht-input v-model="value2" type="password" placeholder="请输入密码" />
			<wht-input v-model="value3" type="number" placeholder="请输入数字" />
			<wht-input v-model="value4" type="digit" placeholder="请输入小数" />
		</view>
		
		<view class="demo-section">
			<view class="demo-title">禁用状态</view>
			<wht-input v-model="value5" disabled placeholder="输入框已禁用" />
		</view>
		
		<view class="demo-section">
			<view class="demo-title">显示清除按钮</view>
			<wht-input v-model="value6" clearable placeholder="请输入文本" />
		</view>
		
		<view class="demo-section">
			<view class="demo-title">带图标的输入框</view>
			<wht-input
				v-model="value7"
				left-icon="search"
				placeholder="请输入搜索关键词"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">错误提示</view>
			<wht-input
				v-model="value8"
				error
				error-message="手机号格式错误"
				placeholder="请输入手机号"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">插入按钮</view>
			<wht-input v-model="sms" placeholder="请输入短信验证码">
				<template #button>
					<wht-button size="small" type="primary" @click="sendSms">
						发送验证码
					</wht-button>
				</template>
			</wht-input>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				value1: '',
				value2: '',
				value3: '',
				value4: '',
				value5: '禁用状态',
				value6: '',
				value7: '',
				value8: '',
				sms: ''
			}
		},
		methods: {
			sendSms() {
				uni.showToast({
					title: '发送验证码',
					icon: 'none'
				})
			}
		}
	}
</script>

<style lang="scss">
.demo-input {
	padding: 20rpx;
	
	.demo-section {
		margin-bottom: 40rpx;
		
		.demo-title {
			font-size: 28rpx;
			color: #666;
			margin-bottom: 20rpx;
		}
		
		.wht-input {
			margin-bottom: 20rpx;
			
			&:last-child {
				margin-bottom: 0;
			}
		}
	}
}
</style>
