<template>
	<view class="demo-notice-bar">
		<view class="demo-section">
			<view class="demo-title">基础用法</view>
			<wht-notice-bar
				text="这是一条基础的通知栏文字内容"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">滚动播放</view>
			<wht-notice-bar
				text="这是一条很长的通知栏文字内容，超出后会自动滚动播放，文字内容比较长所以会滚动"
				:scrollable="true"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">多行展示</view>
			<wht-notice-bar
				text="这是一条很长的通知栏文字内容，可以多行展示，文字内容比较长的时候会自动换行显示，不会溢出"
				:scrollable="false"
				:wrapable="true"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义样式</view>
			<wht-notice-bar
				text="这是一条自定义样式的通知栏文字内容"
				color="#ff6b00"
				background="#fff7e6"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">通知栏模式</view>
			<wht-notice-bar
				text="这是一条可关闭的通知栏"
				mode="closeable"
				@close="onClose"
			/>
			<wht-notice-bar
				text="这是一条可跳转的通知栏"
				mode="link"
				@click="onClick"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义图标</view>
			<wht-notice-bar
				left-icon="volume"
				text="这是一条带有自定义图标的通知栏"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">垂直滚动</view>
			<wht-notice-bar :text="notifications" vertical />
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				notifications: [
					'第一条通知内容',
					'第二条通知内容',
					'第三条通知内容'
				]
			}
		},
		methods: {
			onClose() {
				uni.showToast({
					title: '点击关闭',
					icon: 'none'
				})
			},
			onClick() {
				uni.showToast({
					title: '点击跳转',
					icon: 'none'
				})
			}
		}
	}
</script>

<style lang="scss">
.demo-notice-bar {
	padding: 20rpx;
	
	.demo-section {
		margin-bottom: 40rpx;
		
		.demo-title {
			font-size: 28rpx;
			color: #666;
			margin-bottom: 20rpx;
		}
		
		.wht-notice-bar {
			margin-bottom: 20rpx;
			
			&:last-child {
				margin-bottom: 0;
			}
		}
	}
}
</style>
