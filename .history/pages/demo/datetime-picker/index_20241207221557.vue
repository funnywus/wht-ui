<template>
	<view class="demo-datetime-picker">
		<view class="demo-section">
			<view class="demo-title">选择年月日</view>
			<wht-datetime-picker
				v-model="date"
				type="date"
				title="选择年月日"
				:min-date="minDate"
				:max-date="maxDate"
				@confirm="onConfirm"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">选择年月</view>
			<wht-datetime-picker
				v-model="month"
				type="year-month"
				title="选择年月"
				:min-date="minDate"
				:max-date="maxDate"
				@confirm="onConfirm"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">选择时间</view>
			<wht-datetime-picker
				v-model="time"
				type="time"
				title="选择时间"
				@confirm="onConfirm"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">选择完整时间</view>
			<wht-datetime-picker
				v-model="datetime"
				type="datetime"
				title="选择完整时间"
				:min-date="minDate"
				:max-date="maxDate"
				@confirm="onConfirm"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义列排序</view>
			<wht-datetime-picker
				v-model="customDate"
				type="date"
				title="自定义列排序"
				:columns-order="['month', 'day', 'year']"
				:formatter="formatter"
				@confirm="onConfirm"
			/>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				date: new Date(),
				month: new Date(),
				time: '12:00',
				datetime: new Date(),
				customDate: new Date(),
				minDate: new Date(2020, 0, 1),
				maxDate: new Date(2025, 11, 31)
			}
		},
		methods: {
			onConfirm(value) {
				console.log('selected:', value)
			},
			formatter(type, value) {
				if (type === 'year') {
					return value + '年'
				}
				if (type === 'month') {
					return value + '月'
				}
				if (type === 'day') {
					return value + '日'
				}
				return value
			}
		}
	}
</script>

<style lang="scss">
.demo-datetime-picker {
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
