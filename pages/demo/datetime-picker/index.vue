<template>
	<view class="demo-container">
	  <view class="demo-header">
		<text class="demo-title">wht-datetime-picker</text>
		<text class="demo-subtitle">功能丰富的移动端日期时间选择器</text>
	  </view>
  
	  <view class="demo-section">
		<view class="section-header">
		  <text class="section-title">基础使用</text>
		  <text class="section-subtitle">支持多种选择模式</text>
		</view>
		<view class="demo-block">
		  <view class="demo-cell" @click="showBasic('datetime')">
			<text class="cell-label">日期时间选择</text>
			<view class="cell-value">
			  <text>{{formatDate(basicValue) || '请选择'}}</text>
			  <text class="cell-arrow">></text>
			</view>
		  </view>
		  <view class="demo-cell" @click="showDate('date')">
			<text class="cell-label">日期选择</text>
			<view class="cell-value">
			  <text>{{formatDate(dateValue, 'date') || '请选择'}}</text>
			  <text class="cell-arrow">></text>
			</view>
		  </view>
		  <view class="demo-cell" @click="showTime('time')">
			<text class="cell-label">时间选择</text>
			<view class="cell-value">
			  <text>{{formatDate(timeValue, 'time') || '请选择'}}</text>
			  <text class="cell-arrow">></text>
			</view>
		  </view>
		  <view class="demo-cell" @click="showYear('year')">
			<text class="cell-label">年份选择</text>
			<view class="cell-value">
			  <text>{{formatDate(yearValue, 'year') || '请选择'}}</text>
			  <text class="cell-arrow">></text>
			</view>
		  </view>
		  <view class="demo-cell" @click="showYearMonth('year-month')">
			<text class="cell-label">年月选择</text>
			<view class="cell-value">
			  <text>{{formatDate(yearMonthValue, 'year-month') || '请选择'}}</text>
			  <text class="cell-arrow">></text>
			</view>
		  </view>
		</view>
	  </view>
  
	  <view class="demo-section">
		<view class="section-header">
		  <text class="section-title">区间选择</text>
		  <text class="section-subtitle">支持日期、时间的区间选择</text>
		</view>
		<view class="demo-block">
		  <view class="demo-cell" @click="showRange('datetime-range')">
			<text class="cell-label">日期时间区间</text>
			<view class="cell-value">
			  <text>{{formatDateRange(rangeValue) || '请选择'}}</text>
			  <text class="cell-arrow">></text>
			</view>
		  </view>
		  <view class="demo-cell" @click="showRange('date-range')">
			<text class="cell-label">日期区间</text>
			<view class="cell-value">
			  <text>{{formatDateRange(rangeValue, 'date') || '请选择'}}</text>
			  <text class="cell-arrow">></text>
			</view>
		  </view>
		  <view class="demo-cell" @click="showRange('time-range')">
			<text class="cell-label">时间区间</text>
			<view class="cell-value">
			  <text>{{formatDateRange(rangeValue, 'time') || '请选择'}}</text>
			  <text class="cell-arrow">></text>
			</view>
		  </view>
		</view>
	  </view>
  
	  <view class="demo-section">
		<view class="section-header">
		  <text class="section-title">快捷选项</text>
		  <text class="section-subtitle">支持自定义快捷选项，可设置自动确认</text>
		</view>
		<view class="demo-block">
		  <view class="demo-cell" @click="showQuick('date-range')">
			<text class="cell-label">日期区间快捷选择</text>
			<view class="cell-value">
			  <text>{{formatDateRange(quickValue, 'date') || '请选择'}}</text>
			  <text class="cell-arrow">></text>
			</view>
		  </view>
		</view>
	  </view>
  
	  <wht-datetime-picker
		ref="basicPicker"
		:mode="basicMode"
		:show-seconds="true"
		@confirm="handleBasicConfirm"
	  />
  
	  <wht-datetime-picker
		ref="datePicker"
		:mode="dateMode"
		:show-seconds="true"
		@confirm="handleDateConfirm"
	  />
  
	  <wht-datetime-picker
		ref="timePicker"
		:mode="timeMode"
		:show-seconds="true"
		@confirm="handleTimeConfirm"
	  />
  
	  <wht-datetime-picker
		ref="yearPicker"
		:mode="yearMode"
		:show-seconds="true"
		@confirm="handleYearConfirm"
	  />
  
	  <wht-datetime-picker
		ref="yearMonthPicker"
		:mode="yearMonthMode"
		:show-seconds="true"
		@confirm="handleYearMonthConfirm"
	  />
  
	  <wht-datetime-picker
		ref="rangePicker"
		:mode="rangeMode"
		:show-seconds="true"
		@confirm="handleRangeConfirm"
	  />
  
	  <wht-datetime-picker
		ref="quickPicker"
		:mode="quickMode"
		:show-seconds="true"
		:quick-options="quickOptions"
		@confirm="handleQuickConfirm"
	  />
	</view>
  </template>
  
  <script>
  export default {
	data() {
	  const now = new Date()
	  return {
		// 基础选择
		basicValue: null,
		basicMode: 'datetime',
		
		// 日期选择
		dateValue: null,
		dateMode: 'date',
		
		// 时间选择
		timeValue: null,
		timeMode: 'time',
		
		// 年份选择
		yearValue: null,
		yearMode: 'year',
		
		// 年月选择
		yearMonthValue: null,
		yearMonthMode: 'year-month',
		
		// 区间选择
		rangeValue: null,
		rangeMode: 'datetime-range',
		
		// 快捷选择
		quickValue: null,
		quickMode: 'date-range',
		quickOptions: [
		  {
			label: '今天',
			value: new Date(),
			autoConfirm: true
		  },
		  {
			label: '昨天',
			value: new Date(Date.now() - 24 * 60 * 60 * 1000),
			autoConfirm: true
		  },
		  {
			label: '最近7天',
			value: [
			  new Date(Date.now() - 6 * 24 * 60 * 60 * 1000),
			  new Date()
			]
		  },
		  {
			label: '最近30天',
			value: [
			  new Date(Date.now() - 29 * 24 * 60 * 60 * 1000),
			  new Date()
			]
		  },
		  {
			label: '本月',
			value: [
			  new Date(now.getFullYear(), now.getMonth(), 1),
			  new Date(now.getFullYear(), now.getMonth() + 1, 0)
			]
		  },
		  {
			label: '上月',
			value: [
			  new Date(now.getFullYear(), now.getMonth() - 1, 1),
			  new Date(now.getFullYear(), now.getMonth(), 0)
			]
		  }
		]
	  }
	},
	methods: {
	  // 基础选择
	  showBasic(mode) {
		this.basicMode = mode
		this.$nextTick(() => {
		  this.$refs.basicPicker.show(this.basicValue)
		})
	  },
	  handleBasicConfirm({ value, formatted }) {
		this.basicValue = value
		console.log('基础选择:', formatted)
	  },
	  
	  // 日期选择
	  showDate(mode) {
		this.dateMode = mode
		this.$nextTick(() => {
		  this.$refs.datePicker.show(this.dateValue)
		})
	  },
	  handleDateConfirm({ value, formatted }) {
		this.dateValue = value
		console.log('日期选择:', formatted)
	  },
	  
	  // 时间选择
	  showTime(mode) {
		this.timeMode = mode
		this.$nextTick(() => {
		  this.$refs.timePicker.show(this.timeValue)
		})
	  },
	  handleTimeConfirm({ value, formatted }) {
		this.timeValue = value
		console.log('时间选择:', formatted)
	  },
	  
	  // 年份选择
	  showYear(mode) {
		this.yearMode = mode
		this.$nextTick(() => {
		  this.$refs.yearPicker.show(this.yearValue)
		})
	  },
	  handleYearConfirm({ value, formatted }) {
		this.yearValue = value
		console.log('年份选择:', formatted)
	  },
	  
	  // 年月选择
	  showYearMonth(mode) {
		this.yearMonthMode = mode
		this.$nextTick(() => {
		  this.$refs.yearMonthPicker.show(this.yearMonthValue)
		})
	  },
	  handleYearMonthConfirm({ value, formatted }) {
		this.yearMonthValue = value
		console.log('年月选择:', formatted)
	  },
	  
	  // 区间选择
	  showRange(mode) {
		this.rangeMode = mode
		this.$nextTick(() => {
		  this.$refs.rangePicker.show(this.rangeValue)
		})
	  },
	  handleRangeConfirm({ value, formatted }) {
		this.rangeValue = value
		console.log('区间选择:', formatted)
	  },
	  
	  // 快捷选择
	  showQuick(mode) {
		this.quickMode = mode
		this.$nextTick(() => {
		  this.$refs.quickPicker.show(this.quickValue)
		})
	  },
	  handleQuickConfirm({ value, formatted }) {
		this.quickValue = value
		console.log('快捷选择:', formatted)
	  },
	  
	  // 格式化方法
	  formatDate(date, type = 'datetime') {
		if (!date) return ''
		return this.$refs.basicPicker?.formatDate(date, type) || ''
	  },
	  formatDateRange(dates, type = 'datetime') {
		if (!Array.isArray(dates) || dates.length !== 2) return ''
		return dates.map(date => this.formatDate(date, type)).join(' 至 ')
	  }
	}
  }
  </script>
  
  <style>
  .demo-container {
	min-height: 100vh;
	padding: 30rpx;
	background-color: #f5f6fa;
  }
  
  .demo-header {
	margin-bottom: 40rpx;
	text-align: center;
  }
  
  .demo-title {
	display: block;
	font-size: 48rpx;
	font-weight: bold;
	color: #2c3e50;
	margin-bottom: 16rpx;
	letter-spacing: 1px;
  }
  
  .demo-subtitle {
	font-size: 28rpx;
	color: #7f8c8d;
	letter-spacing: 0.5px;
  }
  
  .demo-section {
	margin-bottom: 40rpx;
  }
  
  .section-header {
	margin: 0 10rpx 20rpx;
  }
  
  .section-title {
	display: block;
	font-size: 32rpx;
	font-weight: bold;
	color: #2c3e50;
	margin-bottom: 8rpx;
  }
  
  .section-subtitle {
	font-size: 26rpx;
	color: #7f8c8d;
  }
  
  .demo-block {
	background: #ffffff;
	border-radius: 16rpx;
	box-shadow: 0 4rpx 12rpx rgba(0, 0, 0, 0.05);
	overflow: hidden;
	transition: all 0.3s ease;
  }
  
  .demo-block:active {
	transform: scale(0.99);
	box-shadow: 0 2rpx 8rpx rgba(0, 0, 0, 0.05);
  }
  
  .demo-cell {
	display: flex;
	align-items: center;
	justify-content: space-between;
	padding: 32rpx 24rpx;
	border-bottom: 1rpx solid #ecf0f1;
	transition: background-color 0.2s ease;
  }
  
  .demo-cell:last-child {
	border-bottom: none;
  }
  
  .demo-cell:active {
	background-color: #f8f9fa;
  }
  
  .cell-label {
	font-size: 28rpx;
	color: #34495e;
	font-weight: 500;
  }
  
  .cell-value {
	display: flex;
	align-items: center;
	font-size: 28rpx;
	color: #7f8c8d;
  }
  
  .cell-arrow {
	margin-left: 12rpx;
	color: #bdc3c7;
	font-family: monospace;
	font-weight: bold;
	transform: scale(0.8, 1.2);
  }
  </style>