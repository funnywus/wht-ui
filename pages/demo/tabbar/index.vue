<template>
	<view class="container">
		<view class="content" v-if="currentTab === 0">
			<text class="title">首页</text>
		</view>
		<view class="content" v-if="currentTab === 1">
			<text class="title">发现</text>
		</view>
		<view class="content" v-if="currentTab === 2">
			<text class="title">发布</text>
		</view>
		<view class="content" v-if="currentTab === 3">
			<text class="title">消息</text>
		</view>
		<view class="content" v-if="currentTab === 4">
			<text class="title">我的</text>
		</view>
		<wht-tabbar v-model:current="currentTab" :centerIndex="2" @click="handleTabClick" />
	</view>
</template>

<script>
	export default {
		data() {
			return {
				currentTab: 0
			}
		},
		methods: {
			handleTabClick(index) {
				console.log('handleTabClick index ', index)
				if (index === 2) {
					// 发布按钮点击
					// 可做弹窗
					uni.showToast({
						title: "凸起"
					})
					return
				}
				this.currentTab = index
			}
		}
	}
</script>

<style>
	.container {
		min-height: 100vh;
		padding-bottom: 100rpx;
	}

	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>