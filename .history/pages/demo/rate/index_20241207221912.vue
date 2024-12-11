<template>
	<view class="demo-rate">
		<view class="demo-section">
			<view class="demo-title">基础用法</view>
			<wht-rate v-model="value1" />
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义图标</view>
			<wht-rate v-model="value2" icon="like" void-icon="like-o" />
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义样式</view>
			<wht-rate
				v-model="value3"
				:size="25"
				color="#ffd21e"
				void-color="#eee"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">半星</view>
			<wht-rate v-model="value4" allow-half />
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义数量</view>
			<wht-rate v-model="value5" :count="6" />
		</view>
		
		<view class="demo-section">
			<view class="demo-title">禁用状态</view>
			<wht-rate v-model="value6" disabled />
		</view>
		
		<view class="demo-section">
			<view class="demo-title">只读状态</view>
			<wht-rate v-model="value7" readonly />
		</view>
		
		<view class="demo-section">
			<view class="demo-title">监听切换事件</view>
			<wht-rate v-model="value8" @change="onChange" />
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				value1: 3,
				value2: 3,
				value3: 3,
				value4: 2.5,
				value5: 4,
				value6: 3,
				value7: 3,
				value8: 3
			}
		},
		methods: {
			onChange(value) {
				uni.showToast({
					title: `当前值：${value}`,
					icon: 'none'
				})
			}
		}
	}
</script>

<style lang="scss">
.demo-rate {
	padding: 20rpx;
	
	.demo-section {
		margin-bottom: 40rpx;
		
		.demo-title {
			font-size: 28rpx;
			color: #666;
			margin-bottom: 20rpx;
		}
	}
}
</style>
