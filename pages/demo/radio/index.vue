<template>
	<view class="content">
		<view class="demo-section">
			<view class="demo-title">普通模式</view>
			<wht-radio
				v-model="value1"
				:options="options"
				@change="onChange"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">列表模式</view>
			<wht-radio
				v-model="value2" 
				type="list"
				:options="options"
				@change="onChange"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义颜色</view>
			<wht-radio
				v-model="value3"
				:options="options"
				color="#FF0000"
			/>
			<wht-radio
				v-model="value4"
				:options="options"
				color="#00FF00"
				style="margin-top: 20rpx;"
			/>
			<wht-radio
				v-model="value5"
				:options="options"
				color="#800080"
				style="margin-top: 20rpx;"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">禁用状态</view>
			<wht-radio
				v-model="value6"
				:options="options"
				disabled
			/>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				value1: '1',
				value2: '2',
				value3: '3',
				value4: '1',
				value5: '2',
				value6: '4',
				options: [
					{ label: '选项1', value: '1' },
					{ label: '选项2', value: '2' },
					{ label: '选项3', value: '3' },
					{ label: '选项4', value: '4' }
				]
			}
		},
		methods: {
			onChange(value) {
				console.log('radio change:', value)
			}
		}
	}
</script>

<style>
	.demo-section {
		margin: 20rpx;
		padding: 20rpx;
		background: #fff;
	}
	.demo-title {
		font-size: 28rpx;
		color: #666;
		margin-bottom: 20rpx;
	}
</style>
