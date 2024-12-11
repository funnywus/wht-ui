<template>
	<view class="demo-checkbox">
		<view class="demo-section">
			<view class="demo-title">基础用法</view>
			<wht-checkbox v-model="checked1">复选框</wht-checkbox>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">禁用状态</view>
			<wht-checkbox v-model="checked2" disabled>禁用状态</wht-checkbox>
			<wht-checkbox v-model="checked3" disabled>选中且禁用</wht-checkbox>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义颜色</view>
			<wht-checkbox v-model="checked4" color="#07c160">自定义颜色</wht-checkbox>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">复选框组</view>
			<wht-checkbox-group v-model="result">
				<wht-checkbox name="a">复选框 a</wht-checkbox>
				<wht-checkbox name="b">复选框 b</wht-checkbox>
				<wht-checkbox name="c">复选框 c</wht-checkbox>
			</wht-checkbox-group>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">限制最大可选数</view>
			<wht-checkbox-group v-model="result2" :max="2">
				<wht-checkbox name="a">复选框 a</wht-checkbox>
				<wht-checkbox name="b">复选框 b</wht-checkbox>
				<wht-checkbox name="c">复选框 c</wht-checkbox>
			</wht-checkbox-group>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				checked1: true,
				checked2: false,
				checked3: true,
				checked4: true,
				result: ['a', 'b'],
				result2: []
			}
		}
	}
</script>

<style lang="scss">
.demo-checkbox {
	padding: 20rpx;
	
	.demo-section {
		margin-bottom: 40rpx;
		
		.demo-title {
			font-size: 28rpx;
			color: #666;
			margin-bottom: 20rpx;
		}
		
		.wht-checkbox {
			margin-bottom: 20rpx;
		}
	}
}
</style>
