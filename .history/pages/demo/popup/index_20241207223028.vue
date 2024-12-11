<template>
	<view class="container">
		<view class="component-title">
			<view class="component-title-content">
				<text class="title">Popup 弹出层</text>
				<text class="desc">弹出层容器，用于展示弹窗、信息提示等内容</text>
			</view>
		</view>

		<view class="card">
			<view class="card-header">
				<text class="card-title">基础用法</text>
				<text class="card-desc">支持多个方向弹出，可自定义内容</text>
			</view>
			<view class="card-content">
				<button class="btn" @click="showCenter = true">居中弹窗</button>
				<button class="btn" @click="showTop = true">顶部弹窗</button>
				<button class="btn" @click="showBottom = true">底部弹窗</button>
				<button class="btn" @click="showLeft = true">左侧弹窗</button>
				<button class="btn" @click="showRight = true">右侧弹窗</button>
			</view>
		</view>

		<wht-popup v-model:show="showCenter" clearable>
			<view class="popup-content">
				<view class="popup-title">标题文字</view>
				<view class="popup-desc">这是一个居中显示的弹窗，点击遮罩或右上角按钮可关闭</view>
			</view>
		</wht-popup>

		<wht-popup v-model:show="showTop" position="top" clearable>
			<view class="popup-content">
				<view class="popup-title">顶部弹窗</view>
				<view class="popup-desc">这是一个从顶部弹出的弹窗</view>
			</view>
		</wht-popup>

		<wht-popup v-model:show="showBottom" position="bottom" clearable>
			<view class="popup-content">
				<view class="popup-title">底部弹窗</view>
				<view class="popup-desc">这是一个从底部弹出的弹窗</view>
			</view>
		</wht-popup>

		<wht-popup v-model:show="showLeft" position="left" clearable>
			<view class="popup-content">
				<view class="popup-title">左侧弹窗</view>
				<view class="popup-desc">这是一个从左侧弹出的弹窗</view>
			</view>
		</wht-popup>

		<wht-popup v-model:show="showRight" position="right" clearable>
			<view class="popup-content">
				<view class="popup-title">右侧弹窗</view>
				<view class="popup-desc">这是一个从右侧弹出的弹窗</view>
			</view>
		</wht-popup>
	</view>
</template>

<script>
export default {
	data() {
		return {
			showCenter: false,
			showTop: false,
			showBottom: false,
			showLeft: false,
			showRight: false
		}
	}
}
</script>

<style lang="scss">
.container {
	padding: 30rpx;
	background: #f5f5f5;
	min-height: 100vh;
}

.component-title {
	padding: 40rpx 30rpx;
	margin: -30rpx -30rpx 30rpx -30rpx;
	border-bottom: 1rpx solid #eee;
	text-align: center;
	.component-title-content {
		background: #fff;
		.title {
			display: block;
			font-size: 40rpx;
			font-weight: 600;
			color: #333;
			margin-bottom: 16rpx;
			line-height: 1.4;
		}
		
		.desc {
			display: block;
			font-size: 28rpx;
			color: #666;
			line-height: 1.6;
		}
	}
}

.card {
	background: #fff;
	border-radius: 16rpx;
	padding: 30rpx;
	margin-bottom: 30rpx;
	box-shadow: 0 4rpx 16rpx rgba(0, 0, 0, 0.08);
}

.card-header {
	padding-bottom: 30rpx;
	border-bottom: 1rpx solid #eee;
	margin-bottom: 30rpx;
}

.card-title {
	display: block;
	font-size: 32rpx;
	font-weight: 600;
	color: #333;
	margin-bottom: 16rpx;
	line-height: 1.4;
}

.card-desc {
	display: block;
	font-size: 28rpx;
	color: #666;
	line-height: 1.5;
}

.card-content {
	display: flex;
	flex-direction: column;
}

.btn {
	margin: 15rpx 0;
	background: #007AFF;
	color: #fff;
	border-radius: 8rpx;
}

/* 弹窗内容样式 */
.popup-content {
	padding: 30rpx;
}

.popup-title {
	font-size: 32rpx;
	font-weight: bold;
	margin-bottom: 20rpx;
	text-align: center;
}

.popup-desc {
	font-size: 28rpx;
	color: #666;
	text-align: center;
}
</style>