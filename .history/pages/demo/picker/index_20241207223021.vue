<template>
	<view class="demo-container">
	  <view class="demo-header">
		<text class="demo-title">WHT Picker 选择器</text>
		<text class="demo-desc">支持单列、多列、级联等多种选择方式的通用选择器组件</text>
	  </view>
	  
	  <!-- 单列选择 -->
	  <view class="demo-card">
		<view class="card-title">单列选择</view>
		<view class="card-desc">最基础的选择器用法</view>
		<view class="card-content">
		  <view class="picker-trigger" @tap="openSinglePicker">
			<text class="trigger-text" :class="{ 'trigger-placeholder': !singleSelected }">
			  {{ singleSelected || '请选择一个选项' }}
			</text>
			<view class="trigger-actions">
			  <text v-if="clearable && singleSelected" class="clear-icon" @tap.stop="clearSinglePicker">×</text>
			  <text v-else class="trigger-icon">></text>
			</view>
		  </view>
		</view>
	  </view>
	  
	  <!-- 多列选择 -->
	  <view class="demo-card">
		<view class="card-title">多列选择</view>
		<view class="card-desc">多个列同时选择，列之间相互独立</view>
		<view class="card-content">
		  <view class="picker-trigger" @tap="openMultiPicker">
			<text class="trigger-text" :class="{ 'trigger-placeholder': !multiSelected }">
			  {{ multiSelected || '请选择多个选项' }}
			</text>
			<view class="trigger-actions">
			  <text v-if="clearable && multiSelected" class="clear-icon" @tap.stop="clearMultiPicker">×</text>
			  <text v-else class="trigger-icon">></text>
			</view>
		  </view>
		</view>
	  </view>
	  
	  <!-- 级联选择 -->
	  <view class="demo-card">
		<view class="card-title">级联选择</view>
		<view class="card-desc">选项之间存在层级关系</view>
		<view class="card-content">
		  <view class="picker-trigger" @tap="openLinkagePicker">
			<text class="trigger-text" :class="{ 'trigger-placeholder': !linkageSelected }">
			  {{ linkageSelected || '请选择一个地区' }}
			</text>
			<view class="trigger-actions">
			  <text v-if="clearable && linkageSelected" class="clear-icon" @tap.stop="clearLinkagePicker">×</text>
			  <text v-else class="trigger-icon">></text>
			</view>
		  </view>
		</view>
	  </view>
	  
	  <!-- 设置值示例 -->
	  <view class="demo-card">
		<view class="card-title">设置值示例</view>
		<view class="card-desc">通过代码设置选择器的值</view>
		<view class="card-content">
		  <view class="button-group">
			<button class="demo-button" @tap="setSingleValue">设置单列值</button>
			<button class="demo-button" @tap="setMultiValue">设置多列值</button>
			<button class="demo-button" @tap="setLinkageValue">设置级联值</button>
		  </view>
		</view>
	  </view>
	  
	  <!-- 选择器组件 -->
	  <wht-picker
		ref="singlePicker"
		v-model="singleValue"
		:columns="singleColumns"
		:clearable="clearable"
		type="single"
		indicator-style="height: 100rpx; line-height: 100rpx;"
		@confirm="onSingleConfirm"
		@clear="onSingleClear"
	  />
	  
	  <wht-picker
		ref="multiPicker"
		v-model="multiValue"
		:columns="multiColumns"
		:clearable="clearable"
		type="multi"
		@confirm="onMultiConfirm"
		@clear="onMultiClear"
	  />
	  
	  <wht-picker
		ref="linkagePicker"
		v-model="linkageValue"
		:columns="linkageColumns"
		:clearable="clearable"
		type="linkage"
		@confirm="onLinkageConfirm"
		@clear="onLinkageClear"
	  />
	</view>
  </template>
  
  <script>
  export default {
	data() {
	  return {
		clearable: true,
		// 单列选择
		singleValue: [],
		singleSelected: '',
		singleColumns: [
		  { label: '选项1', value: 1 },
		  { label: '选项2', value: 2 },
		  { label: '选项3', value: 3 },
		  { label: '选项4', value: 4 }
		],
		
		// 多列选择
		multiValue: [],
		multiSelected: '',
		multiColumns: [
		  [
			{ label: 'A', value: 'A' },
			{ label: 'B', value: 'B' },
			{ label: 'C', value: 'C' }
		  ],
		  [
			{ label: '1', value: 1 },
			{ label: '2', value: 2 },
			{ label: '3', value: 3 }
		  ]
		],
		
		// 级联选择
		linkageValue: [],
		linkageSelected: '',
		linkageColumns: [
		  {
			label: '浙江',
			value: 'zj',
			children: [
			  {
				label: '杭州',
				value: 'hz',
				children: [
				  { label: '西湖区', value: 'xh' },
				  { label: '余杭区', value: 'yh' }
				]
			  },
			  {
				label: '宁波',
				value: 'nb',
				children: [
				  { label: '海曙区', value: 'hs' },
				  { label: '江北区', value: 'jb' }
				]
			  }
			]
		  },
		  {
			label: '江苏',
			value: 'js',
			children: [
			  {
				label: '南京',
				value: 'nj',
				children: [
				  { label: '玄武区', value: 'xw' },
				  { label: '秦淮区', value: 'qh' }
				]
			  }
			]
		  }
		]
	  }
	},
	
	methods: {
	  // 打开选择器方法
	  openSinglePicker() {
		this.$refs.singlePicker.open()
	  },
	  
	  openMultiPicker() {
		this.$refs.multiPicker.open()
	  },
	  
	  openLinkagePicker() {
		this.$refs.linkagePicker.open()
	  },
	  
	  // 确认回调方法
	  onSingleConfirm(e) {
		this.singleSelected = e.display
		console.log('单列选择结果：', e)
	  },
	  
	  onMultiConfirm(e) {
		this.multiSelected = e.display
		console.log('多列选择结果：', e)
	  },
	  
	  onLinkageConfirm(e) {
		this.linkageSelected = e.display
		console.log('级联选择结果：', e)
	  },
	  
	  // 设置值方法
	  setSingleValue() {
		this.$refs.singlePicker.setValue([1])
	  },
	  
	  setMultiValue() {
		this.$refs.multiPicker.setValue([1, 1])
	  },
	  
	  setLinkageValue() {
		this.$refs.linkagePicker.setValue([0, 0, 1])
	  },
	  
	  // 清空方法
	  clearSinglePicker(e) {
		e.stopPropagation()
		this.$refs.singlePicker.clear()
		this.singleSelected = ''
	  },
	  
	  clearMultiPicker(e) {
		e.stopPropagation()
		this.$refs.multiPicker.clear()
		this.multiSelected = ''
	  },
	  
	  clearLinkagePicker(e) {
		e.stopPropagation()
		this.$refs.linkagePicker.clear()
		this.linkageSelected = ''
	  },
	  
	  // 清空事件处理
	  onSingleClear() {
		this.singleSelected = ''
	  },
	  
	  onMultiClear() {
		this.multiSelected = ''
	  },
	  
	  onLinkageClear() {
		this.linkageSelected = ''
	  }
	}
  }
  </script>
  
  <style>
  .demo-container {
	padding: 20rpx;
	background-color: #f5f5f5;
	min-height: 100vh;
  }
  
  .demo-header {
	padding: 40rpx 20rpx;
	text-align: center;
	margin-bottom: 30rpx;
  }
  
  .demo-title {
	font-size: 40rpx;
	font-weight: bold;
	color: #333;
	margin-bottom: 16rpx;
	display: block;
  }
  
  .demo-desc {
	font-size: 28rpx;
	color: #666;
	display: block;
  }
  
  .demo-card {
	background-color: #fff;
	border-radius: 16rpx;
	padding: 30rpx;
	margin-bottom: 30rpx;
	box-shadow: 0 2rpx 12rpx rgba(0, 0, 0, 0.05);
  }
  
  .card-title {
	font-size: 32rpx;
	font-weight: 500;
	color: #333;
	margin-bottom: 16rpx;
  }
  
  .card-desc {
	font-size: 26rpx;
	color: #999;
	margin-bottom: 30rpx;
  }
  
  .card-content {
	position: relative;
  }
  
  .picker-trigger {
	height: 88rpx;
	display: flex;
	align-items: center;
	justify-content: space-between;
	padding: 0 30rpx;
	background-color: #f8f8f8;
	border-radius: 8rpx;
	border: 1rpx solid #ddd;
	transition: background-color 0.3s, border-color 0.3s;
  }
  
  .picker-trigger:active {
	background-color: #e0e0e0;
	border-color: #ccc;
  }
  
  .trigger-text {
	font-size: 28rpx;
	color: #333;
  }
  
  .trigger-icon {
	color: #999;
	transform: rotate(90deg);
	transition: transform 0.3s;
  }
  
  .button-group {
	display: flex;
	flex-wrap: wrap;
	gap: 20rpx;
  }
  
  .demo-button {
	flex: 1;
	min-width: 200rpx;
	height: 80rpx;
	line-height: 80rpx;
	text-align: center;
	background-color: #007AFF;
	color: #fff;
	border-radius: 8rpx;
	font-size: 28rpx;
  }
  
  .demo-button:active {
	opacity: 0.8;
  }
  
  .trigger-actions {
	display: flex;
	align-items: center;
	gap: 10rpx;
  }
  
  .clear-icon {
	display: flex;
	align-items: center;
	justify-content: center;
	width: 44rpx;
	height: 44rpx;
	font-size: 32rpx;
	color: #999;
	border-radius: 50%;
	background-color: #f0f0f0;
	transition: all 0.3s;
  }
  
  .clear-icon:active {
	background-color: #e0e0e0;
	transform: scale(0.9);
  }
  
 
  </style>