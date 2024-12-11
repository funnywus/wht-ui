<template>
	<view class="demo-tabs">
		<view class="demo-section">
			<view class="demo-title">基础用法</view>
			<wht-tabs v-model="active1">
				<wht-tab title="标签 1">内容 1</wht-tab>
				<wht-tab title="标签 2">内容 2</wht-tab>
				<wht-tab title="标签 3">内容 3</wht-tab>
			</wht-tabs>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">通过名称匹配</view>
			<wht-tabs v-model="active2">
				<wht-tab title="标签 1" name="a">内容 1</wht-tab>
				<wht-tab title="标签 2" name="b">内容 2</wht-tab>
				<wht-tab title="标签 3" name="c">内容 3</wht-tab>
			</wht-tabs>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">标签栏滚动</view>
			<wht-tabs v-model="active3">
				<wht-tab v-for="index in 8" :key="index" :title="'标签 ' + index">
					内容 {{ index }}
				</wht-tab>
			</wht-tabs>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">禁用标签</view>
			<wht-tabs v-model="active4">
				<wht-tab title="标签 1">内容 1</wht-tab>
				<wht-tab title="标签 2" disabled>内容 2</wht-tab>
				<wht-tab title="标签 3">内容 3</wht-tab>
			</wht-tabs>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">样式风格</view>
			<wht-tabs v-model="active5" type="card">
				<wht-tab title="标签 1">内容 1</wht-tab>
				<wht-tab title="标签 2">内容 2</wht-tab>
				<wht-tab title="标签 3">内容 3</wht-tab>
			</wht-tabs>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">点击事件</view>
			<wht-tabs v-model="active6" @click="onClick">
				<wht-tab title="标签 1">内容 1</wht-tab>
				<wht-tab title="标签 2">内容 2</wht-tab>
				<wht-tab title="标签 3">内容 3</wht-tab>
			</wht-tabs>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">粘性布局</view>
			<wht-tabs v-model="active7" sticky>
				<wht-tab title="标签 1">内容 1</wht-tab>
				<wht-tab title="标签 2">内容 2</wht-tab>
				<wht-tab title="标签 3">内容 3</wht-tab>
			</wht-tabs>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义标签</view>
			<wht-tabs v-model="active8">
				<wht-tab v-for="index in 3" :key="index">
					<template #title>
						<view class="custom-tab">
							<text class="tab-text">标签 {{ index }}</text>
							<text class="tab-count">{{ index }}</text>
						</view>
					</template>
					内容 {{ index }}
				</wht-tab>
			</wht-tabs>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				active1: 0,
				active2: 'a',
				active3: 0,
				active4: 0,
				active5: 0,
				active6: 0,
				active7: 0,
				active8: 0
			}
		},
		methods: {
			onClick(index) {
				uni.showToast({
					title: `点击标签 ${index + 1}`,
					icon: 'none'
				})
			}
		}
	}
</script>

<style lang="scss">
.demo-tabs {
	padding: 20rpx;
	
	.demo-section {
		margin-bottom: 40rpx;
		
		.demo-title {
			font-size: 28rpx;
			color: #666;
			margin-bottom: 20rpx;
		}
		
		.custom-tab {
			display: flex;
			align-items: center;
			justify-content: center;
			
			.tab-text {
				margin-right: 8rpx;
			}
			
			.tab-count {
				font-size: 24rpx;
				background-color: #ee0a24;
				color: #fff;
				border-radius: 12rpx;
				padding: 0 8rpx;
				min-width: 24rpx;
				text-align: center;
			}
		}
	}
}
</style>
