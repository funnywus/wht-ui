<template>
	<view class="demo-button">
		<view class="demo-section">
			<view class="demo-title">按钮类型</view>
			<view class="button-group">
				<wht-button>默认按钮</wht-button>
				<wht-button type="primary">主要按钮</wht-button>
				<wht-button type="success">成功按钮</wht-button>
				<wht-button type="warning">警告按钮</wht-button>
				<wht-button type="danger">危险按钮</wht-button>
			</view>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">朴素按钮</view>
			<view class="button-group">
				<wht-button plain>朴素按钮</wht-button>
				<wht-button type="primary" plain>主要按钮</wht-button>
				<wht-button type="success" plain>成功按钮</wht-button>
			</view>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">禁用状态</view>
			<view class="button-group">
				<wht-button disabled>禁用按钮</wht-button>
				<wht-button type="primary" disabled>禁用按钮</wht-button>
			</view>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">加载状态</view>
			<view class="button-group">
				<wht-button loading>加载中...</wht-button>
				<wht-button type="primary" loading>加载中...</wht-button>
			</view>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">按钮形状</view>
			<view class="button-group">
				<wht-button round>圆角按钮</wht-button>
				<wht-button type="primary" round>圆角按钮</wht-button>
			</view>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">按钮尺寸</view>
			<view class="button-group">
				<wht-button size="large">大号按钮</wht-button>
				<wht-button>普通按钮</wht-button>
				<wht-button size="small">小型按钮</wht-button>
				<wht-button size="mini">迷你按钮</wht-button>
			</view>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">点击事件</view>
			<wht-button type="primary" @click="onClick">点击按钮</wht-button>
		</view>
	</view>
</template>

<script>
	export default {
		methods: {
			onClick() {
				uni.showToast({
					title: '点击按钮',
					icon: 'none'
				})
			}
		}
	}
</script>

<style lang="scss">
.demo-button {
	padding: 20rpx;
	
	.demo-section {
		margin-bottom: 40rpx;
		
		.demo-title {
			font-size: 28rpx;
			color: #666;
			margin-bottom: 20rpx;
		}
		
		.button-group {
			.wht-button {
				margin: 0 20rpx 20rpx 0;
				
				&:last-child {
					margin-right: 0;
				}
			}
		}
	}
}
</style>
