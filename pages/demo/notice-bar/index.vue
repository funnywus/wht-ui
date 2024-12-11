<template>
	<view class="demo">
		<view class="demo-header">
			<view class="demo-header__title">通知栏 Notice Bar</view>
			<view class="demo-header__desc">
				用于循环播放展示一组消息通知，可自定义样式、滚动速度等。常用于消息提醒、活动通知等场景。
			</view>
		</view>
		
		<view class="demo-card">
			<view class="demo-card__title">基础用法</view>
			<view class="demo-card__desc">最基础的通知栏用法，展示通知内容。</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar text="这是一条基础通知栏消息"></wht-notice-bar>
			</view>
		</view>
		
		<view class="demo-card">
			<view class="demo-card__title">主题类型</view>
			<view class="demo-card__desc">通知栏支持多种主题类型：primary、success、warning、error、info。</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar text="主要通知" type="primary"></wht-notice-bar>
			</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar text="成功通知" type="success"></wht-notice-bar>
			</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar text="警告通知" type="warning"></wht-notice-bar>
			</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar text="错误通知" type="error"></wht-notice-bar>
			</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar text="信息通知" type="info"></wht-notice-bar>
			</view>
		</view>
		
		<view class="demo-card">
			<view class="demo-card__title">自定义样式</view>
			<view class="demo-card__desc">可以自定义背景色和文字颜色。</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar 
					text="自定义背景色和文字颜色" 
					bgColor="#f0f9eb" 
					color="#67c23a">
				</wht-notice-bar>
			</view>
		</view>
		
		<view class="demo-card">
			<view class="demo-card__title">图标控制</view>
			<view class="demo-card__desc">可以控制左侧图标和右侧关闭按钮的显示。</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar 
					text="不显示左侧图标" 
					:showIcon="false">
				</wht-notice-bar>
			</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar 
					text="显示关闭按钮" 
					:showClose="true">
				</wht-notice-bar>
			</view>
		</view>
		
		<view class="demo-card">
			<view class="demo-card__title">滚动控制</view>
			<view class="demo-card__desc">可以控制是否开启滚动和滚动速度。</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar 
					text="这条通知即使文字超出也不会滚动，将显示省略号" 
					:scrollable="true"
					:speed="50"
					>
				</wht-notice-bar>
			</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar 
					text="速度较慢的滚动通知消息" 
					:scrollable="true"
					:speed="50">
				</wht-notice-bar>
			</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar 
					text="速度较快的滚动通知消息" 
					:scrollable="true"
					:speed="200">
				</wht-notice-bar>
			</view>
		</view>
		
		<view class="demo-card">
			<view class="demo-card__title">单行/多行切换</view>
			<view class="demo-card__desc">可以设置单行滚动或多行显示模式。</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar 
					text="这是一条单行滚动的通知消息" 
					:single="true">
				</wht-notice-bar>
			</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar 
					text="这是一条多行显示的通知消息，可以完整显示较长的内容。这是一条多行显示的通知消息，可以完整显示较长的内容。" 
					:single="false" 
					:rows="3">
				</wht-notice-bar>
			</view>
		</view>
		
		<view class="demo-card">
			<view class="demo-card__title">事件监听</view>
			<view class="demo-card__desc">支持点击内容和关闭按钮的事件监听。</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar 
					text="点击查看详情" 
					@click="handleClick">
				</wht-notice-bar>
			</view>
			<view class="demo-notice-wrap">
				<wht-notice-bar 
					text="点击关闭按钮试试" 
					:showClose="true" 
					@close="handleClose">
				</wht-notice-bar>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {

		},
		methods: {
			handleClick() {
				uni.showToast({
					title: '点击了通知栏',
					icon: 'none'
				})
			},
			handleClose() {
				uni.showToast({
					title: '关闭了通知栏',
					icon: 'none'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.demo {
		padding: 20rpx;
		background-color: #f5f5f5;
		
		&-header {
			padding: 40rpx 30rpx;
			background-color: #fff;
			margin-bottom: 20rpx;
			border-radius: 16rpx;
			
			&__title {
				font-size: 40rpx;
				font-weight: bold;
				color: #333;
				margin-bottom: 16rpx;
			}
			
			&__desc {
				font-size: 28rpx;
				color: #666;
				line-height: 1.5;
			}
		}
	}

	.demo-card {
		margin-bottom: 30rpx;
		padding: 30rpx;
		background-color: #fff;
		border-radius: 16rpx;
		box-shadow: 0 4rpx 8rpx rgba(0, 0, 0, 0.1);
		
		&__title {
			font-size: 32rpx;
			font-weight: bold;
			margin-bottom: 16rpx;
			color: #333;
		}
		
		&__desc {
			font-size: 28rpx;
			color: #666;
			margin-bottom: 20rpx;
			line-height: 1.5;
		}
	}

	.demo-notice-wrap {
		margin-bottom: 20rpx;
		
		&:last-child {
			margin-bottom: 0;
		}
	}
</style>
