<template>
	<view class="demo-search">
		<view class="demo-section">
			<view class="demo-title">基础用法</view>
			<wht-search v-model="value1" placeholder="请输入搜索关键词" />
		</view>
		
		<view class="demo-section">
			<view class="demo-title">事件监听</view>
			<wht-search
				v-model="value2"
				placeholder="请输入搜索关键词"
				@search="onSearch"
				@cancel="onCancel"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">搜索框内容对齐</view>
			<wht-search
				v-model="value3"
				input-align="center"
				placeholder="请输入搜索关键词"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">禁用搜索框</view>
			<wht-search
				v-model="value4"
				disabled
				placeholder="请输入搜索关键词"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义背景色</view>
			<wht-search
				v-model="value5"
				placeholder="请输入搜索关键词"
				background="#4fc08d"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义按钮</view>
			<wht-search
				v-model="value6"
				placeholder="请输入搜索关键词"
				show-action
				@search="onSearch"
				@cancel="onCancel"
			>
				<template #action>
					<view class="custom-action" @click="onSearch">搜索</view>
				</template>
			</wht-search>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">搜索框形状</view>
			<wht-search
				v-model="value7"
				shape="round"
				placeholder="请输入搜索关键词"
			/>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				value1: '',
				value2: '',
				value3: '',
				value4: '',
				value5: '',
				value6: '',
				value7: ''
			}
		},
		methods: {
			onSearch(val) {
				uni.showToast({
					title: `搜索：${val}`,
					icon: 'none'
				})
			},
			onCancel() {
				uni.showToast({
					title: '取消搜索',
					icon: 'none'
				})
			}
		}
	}
</script>

<style lang="scss">
.demo-search {
	padding: 20rpx;
	
	.demo-section {
		margin-bottom: 40rpx;
		
		.demo-title {
			font-size: 28rpx;
			color: #666;
			margin-bottom: 20rpx;
		}
		
		.custom-action {
			padding: 0 20rpx;
			height: 100%;
			display: flex;
			align-items: center;
			color: #323233;
		}
	}
}
</style>
