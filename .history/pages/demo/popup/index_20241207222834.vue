<template>
	<view class="demo-popup">
		<view class="demo-section">
			<view class="demo-title">基础用法</view>
			<wht-button type="primary" @click="showBasic = true">展示弹出层</wht-button>
			<wht-popup v-model="showBasic">
				<view class="popup-content">内容</view>
			</wht-popup>
		
		<view class="demo-section">
			<view class="demo-title">弹出位置</view>
			<view class="button-group">
				<wht-button @click="showTop = true">顶部弹出</wht-button>
				<wht-button @click="showBottom = true">底部弹出</wht-button>
				<wht-button @click="showLeft = true">左侧弹出</wht-button>
				<wht-button @click="showRight = true">右侧弹出</wht-button>
			</view>
			
			<wht-popup v-model="showTop" position="top">
				<view class="popup-content">顶部弹出</view>
			</wht-popup>
			
			<wht-popup v-model="showBottom" position="bottom">
				<view class="popup-content">底部弹出</view>
			</wht-popup>
			
			<wht-popup v-model="showLeft" position="left">
				<view class="popup-content">左侧弹出</view>
			</wht-popup>
			
			<wht-popup v-model="showRight" position="right">
				<view class="popup-content">右侧弹出</view>
			</wht-popup>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">圆角弹窗</view>
			<wht-button @click="showRound = true">圆角弹窗</wht-button>
			<wht-popup v-model="showRound" round position="bottom">
				<view class="popup-content">圆角弹窗</view>
			</wht-popup>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">关闭图标</view>
			<wht-button @click="showCloseIcon = true">关闭图标</wht-button>
			<wht-popup
				v-model="showCloseIcon"
				closeable
				position="bottom"
				:style="{ height: '30%' }"
			>
				<view class="popup-content">关闭图标</view>
			</wht-popup>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义内容</view>
			<wht-button @click="showCustom = true">自定义内容</wht-button>
			<wht-popup
				v-model="showCustom"
				closeable
				round
				position="bottom"
				:style="{ height: '40%' }"
			>
				<view class="custom-popup">
					<view class="custom-title">标题</view>
					<view class="custom-content">
						这是一段自定义内容
					</view>
					<view class="custom-footer">
						<wht-button @click="showCustom = false">关闭</wht-button>
						<wht-button type="primary" @click="onConfirm">确认</wht-button>
					</view>
				</view>
			</wht-popup>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				showBasic: false,
				showTop: false,
				showBottom: false,
				showLeft: false,
				showRight: false,
				showRound: false,
				showCloseIcon: false,
				showCustom: false
			}
		},
		methods: {
			onConfirm() {
				this.showCustom = false
				uni.showToast({
					title: '点击确认',
					icon: 'none'
				})
			}
		}
	}
</script>

<style lang="scss">
.demo-popup {
	padding: 20rpx;
	
	.demo-section {
		margin-bottom: 40rpx;
		
		.demo-title {
			font-size: 28rpx;
			color: #666;
			margin-bottom: 20rpx;
		}
		
		.button-group {
			display: flex;
			flex-wrap: wrap;
			margin: 0 -10rpx;
			
			.wht-button {
				margin: 10rpx;
				flex: 1;
			}
		}
	}
	
	.popup-content {
		padding: 30rpx;
		min-height: 200rpx;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	
	.custom-popup {
		padding: 30rpx;
		
		.custom-title {
			text-align: center;
			font-size: 32rpx;
			font-weight: bold;
			color: #323233;
			margin-bottom: 20rpx;
		}
		
		.custom-content {
			min-height: 200rpx;
			display: flex;
			align-items: center;
			justify-content: center;
			color: #666;
		}
		
		.custom-footer {
			display: flex;
			padding-top: 20rpx;
			
			.wht-button {
				flex: 1;
				margin: 0 10rpx;
			}
		}
	}
}
</style>
