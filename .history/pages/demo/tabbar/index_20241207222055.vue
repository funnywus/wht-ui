<template>
	<view class="demo-tabbar">
		<view class="demo-section">
			<view class="demo-title">基础用法</view>
			<wht-tabbar v-model="active1">
				<wht-tabbar-item icon="home">首页</wht-tabbar-item>
				<wht-tabbar-item icon="search">搜索</wht-tabbar-item>
				<wht-tabbar-item icon="user">我的</wht-tabbar-item>
			</wht-tabbar>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义颜色</view>
			<wht-tabbar
				v-model="active2"
				active-color="#07c160"
				inactive-color="#000"
			>
				<wht-tabbar-item icon="home">首页</wht-tabbar-item>
				<wht-tabbar-item icon="search">搜索</wht-tabbar-item>
				<wht-tabbar-item icon="user">我的</wht-tabbar-item>
			</wht-tabbar>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义图标</view>
			<wht-tabbar v-model="active3">
				<wht-tabbar-item>
					<image
						slot="icon"
						class="icon"
						:src="active3 === 0 ? icon.active : icon.inactive"
					/>
					<image
						slot="icon-active"
						class="icon"
						:src="icon.active"
					/>
					自定义
				</wht-tabbar-item>
				<wht-tabbar-item icon="search">搜索</wht-tabbar-item>
				<wht-tabbar-item icon="user">我的</wht-tabbar-item>
			</wht-tabbar>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">徽标提示</view>
			<wht-tabbar v-model="active4">
				<wht-tabbar-item icon="home" dot>首页</wht-tabbar-item>
				<wht-tabbar-item icon="search" badge="5">搜索</wht-tabbar-item>
				<wht-tabbar-item icon="user" badge="20">我的</wht-tabbar-item>
			</wht-tabbar>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">监听切换事件</view>
			<wht-tabbar v-model="active5" @change="onChange">
				<wht-tabbar-item icon="home">首页</wht-tabbar-item>
				<wht-tabbar-item icon="search">搜索</wht-tabbar-item>
				<wht-tabbar-item icon="user">我的</wht-tabbar-item>
			</wht-tabbar>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				active1: 0,
				active2: 0,
				active3: 0,
				active4: 0,
				active5: 0,
				icon: {
					active: '/static/tabbar/home-active.png',
					inactive: '/static/tabbar/home.png'
				}
			}
		},
		methods: {
			onChange(index) {
				uni.showToast({
					title: `切换到标签 ${index + 1}`,
					icon: 'none'
				})
			}
		}
	}
</script>

<style lang="scss">
.demo-tabbar {
	padding: 20rpx;
	padding-bottom: 150rpx;
	
	.demo-section {
		margin-bottom: 40rpx;
		
		.demo-title {
			font-size: 28rpx;
			color: #666;
			margin-bottom: 20rpx;
		}
		
		.icon {
			width: 48rpx;
			height: 48rpx;
		}
	}
	
	.wht-tabbar {
		position: relative !important;
		margin-top: 20rpx;
	}
}
</style>
