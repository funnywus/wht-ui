<template>
	<view class="demo-picker">
		<view class="demo-section">
			<view class="demo-title">基础用法</view>
			<wht-picker
				:columns="columns1"
				@change="onChange"
				@confirm="onConfirm"
				@cancel="onCancel"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">默认选中项</view>
			<wht-picker
				:columns="columns1"
				:default-index="2"
				@change="onChange"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">多列选择</view>
			<wht-picker
				:columns="columns2"
				@change="onChange"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">级联选择</view>
			<wht-picker
				:columns="columns3"
				@change="onChange"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">禁用选项</view>
			<wht-picker
				:columns="columns4"
				@change="onChange"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">加载状态</view>
			<wht-picker
				:columns="columns1"
				loading
			/>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				columns1: ['杭州', '宁波', '温州', '嘉兴', '湖州'],
				columns2: [
					['周一', '周二', '周三', '周四', '周五'],
					['上午', '下午', '晚上']
				],
				columns3: {
					province_list: {
						110000: '北京市',
						120000: '天津市'
					},
					city_list: {
						110100: '北京市',
						120100: '天津市'
					},
					county_list: {
						110101: '东城区',
						110102: '西城区',
						120101: '和平区',
						120102: '河东区'
					}
				},
				columns4: [
					{ text: '杭州', disabled: false },
					{ text: '宁波', disabled: true },
					{ text: '温州', disabled: false }
				]
			}
		},
		methods: {
			onChange(event) {
				console.log('onChange:', event)
			},
			onConfirm(event) {
				console.log('onConfirm:', event)
			},
			onCancel() {
				console.log('onCancel')
			}
		}
	}
</script>

<style lang="scss">
.demo-picker {
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
