<template>
	<view class="demo-radio">
		<view class="demo-section">
			<view class="demo-title">基础用法</view>
			<wht-radio-group v-model="radio1">
				<wht-radio name="1">单选框 1</wht-radio>
				<wht-radio name="2">单选框 2</wht-radio>
			</wht-radio-group>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">水平排列</view>
			<wht-radio-group v-model="radio2" direction="horizontal">
				<wht-radio name="1">单选框 1</wht-radio>
				<wht-radio name="2">单选框 2</wht-radio>
			</wht-radio-group>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">禁用状态</view>
			<wht-radio-group v-model="radio3">
				<wht-radio name="1" disabled>禁用单选框</wht-radio>
				<wht-radio name="2" disabled>禁用单选框</wht-radio>
			</wht-radio-group>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义颜色</view>
			<wht-radio-group v-model="radio4">
				<wht-radio name="1" checked-color="#07c160">自定义颜色</wht-radio>
				<wht-radio name="2" checked-color="#07c160">自定义颜色</wht-radio>
			</wht-radio-group>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义大小</view>
			<wht-radio-group v-model="radio5">
				<wht-radio name="1" icon-size="24">自定义大小</wht-radio>
				<wht-radio name="2" icon-size="24">自定义大小</wht-radio>
			</wht-radio-group>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义形状</view>
			<wht-radio-group v-model="radio6">
				<wht-radio name="1" shape="square">自定义形状</wht-radio>
				<wht-radio name="2" shape="square">自定义形状</wht-radio>
			</wht-radio-group>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">监听切换事件</view>
			<wht-radio-group v-model="radio7" @change="onChange">
				<wht-radio name="1">单选框 1</wht-radio>
				<wht-radio name="2">单选框 2</wht-radio>
			</wht-radio-group>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				radio1: '1',
				radio2: '1',
				radio3: '1',
				radio4: '1',
				radio5: '1',
				radio6: '1',
				radio7: '1'
			}
		},
		methods: {
			onChange(event) {
				uni.showToast({
					title: `选中值: ${event}`,
					icon: 'none'
				})
			}
		}
	}
</script>

<style lang="scss">
.demo-radio {
	padding: 20rpx;
	
	.demo-section {
		margin-bottom: 40rpx;
		
		.demo-title {
			font-size: 28rpx;
			color: #666;
			margin-bottom: 20rpx;
		}
		
		.wht-radio {
			margin-bottom: 20rpx;
			
			&:last-child {
				margin-bottom: 0;
			}
		}
	}
}
</style>
