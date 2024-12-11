<template>
	<view class="container">
	  <view class="page-title">老虎机抽奖 Demo</view>
	  
	  <!-- 基础抽奖 -->
	  <view class="lottery-box">
		<text class="title">基础抽奖</text>
		<wht-lottery ref="lottery1" @finish="onLotteryFinish" />
		<view class="btn-group">
		  <button 
			class="btn"
			:disabled="isSpinning1" 
			@click="handleStart1"
		  >
			{{ isSpinning1 ? '抽奖中...' : '开始抽奖' }}
		  </button>
		</view>
	  </view>
	  
	  <!-- 自定义抽奖 -->
	  <view class="lottery-box">
		<text class="title">自定义抽奖</text>
		<wht-lottery 
		  ref="lottery2"
		  :columns="3"
		  :column-values="customValues"
		  @finish="onLotteryFinish"
		/>
		<view class="preset-list">
		  <view 
			v-for="(item, index) in presetResults" 
			:key="index"
			class="preset-item"
			:class="{ active: selectedResult === item }"
			@click="selectResult(item)"
		  >
			{{ item }}
		  </view>
		</view>
		<view class="btn-group">
		  <button 
			class="btn"
			:disabled="isSpinning2" 
			@click="handleStart2"
		  >
			{{ isSpinning2 ? '抽奖中...' : '开始抽奖' }}
		  </button>
		</view>
	  </view>
	</view>
  </template>
  
  <script>
  export default {
	data() {
	  return {
		isSpinning1: false,
		isSpinning2: false,
		selectedResult: '',
		// 自定义转轮数据
		customValues: [
		  ['金', '银', '铜'],
		  ['特', '一', '二'],
		  ['奖', '奖', '奖']
		],
		// 预设结果
		presetResults: ['金特奖', '银一奖', '铜二奖']
	  }
	},
	methods: {
	  // 基础抽奖
	  handleStart1() {
		if (this.isSpinning1) return
		this.isSpinning1 = true
		
		// 随机生成结果
		const result = this.generateRandomResult()
		this.$refs.lottery1.start(result)
		
		setTimeout(() => {
		  this.isSpinning1 = false
		  uni.showToast({
			title: `抽中：${result}`,
			icon: 'none'
		  })
		}, 4000)
	  },
	  
	  // 生成随机结果
	  generateRandomResult() {
		const defaultValues = [
		  ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'],
		  ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J'],
		  ['红', '橙', '黄', '绿', '青', '蓝', '紫'],
		  ['♠', '♥', '♣', '♦']
		]
		
		return defaultValues.map(column => 
		  column[Math.floor(Math.random() * column.length)]
		).join('')
	  },
	  
	  // 选择预设结果
	  selectResult(result) {
		if (this.isSpinning2) return
		this.selectedResult = result
	  },
	  
	  // 自定义抽奖
	  handleStart2() {
		if (this.isSpinning2 || !this.selectedResult) return
		this.isSpinning2 = true
		
		this.$refs.lottery2.start(this.selectedResult)
		
		setTimeout(() => {
		  this.isSpinning2 = false
		  uni.showToast({
			title: `抽中：${this.selectedResult}`,
			icon: 'none'
		  })
		}, 4000)
	  },
	  
	  // 抽奖结束回调
	  onLotteryFinish(result) {
		console.log('抽奖结束 ', result)
	  }
	}
  }
  </script>
  
  <style>
  .container {
	padding: 40rpx;
	background: #f5f5f5;
	min-height: 100vh;
  }
  
  .lottery-box {
	margin-bottom: 60rpx;
	background: #fff;
	padding: 40rpx;
	border-radius: 24rpx;
	box-shadow: 0 4rpx 16rpx rgba(0, 0, 0, 0.05);
  }
  
  .title {
	display: block;
	font-size: 32rpx;
	font-weight: 500;
	color: #333;
	margin-bottom: 40rpx;
	text-align: center;
  }
  
  .btn-group {
	margin-top: 40rpx;
  }
  
  .btn {
	width: 100%;
	height: 88rpx;
	line-height: 88rpx;
	background: #000;
	color: #fff;
	font-size: 32rpx;
	border: none;
	border-radius: 12rpx;
  }
  
  .btn:active {
	opacity: 0.8;
  }
  
  .btn[disabled] {
	background: #999;
	opacity: 0.6;
  }
  
  .preset-list {
	display: flex;
	flex-wrap: wrap;
	gap: 20rpx;
	margin-top: 40rpx;
  }
  
  .preset-item {
	flex: 1;
	min-width: 160rpx;
	padding: 20rpx;
	text-align: center;
	background: #f8f8f8;
	border: 2rpx solid #eee;
	border-radius: 12rpx;
	font-size: 28rpx;
	color: #333;
  }
  
  .preset-item.active {
	background: #000;
	border-color: #000;
	color: #fff;
  }
  
  .preset-item:active {
	opacity: 0.8;
  }
  
  .page-title {
	font-size: 40rpx;
	font-weight: bold;
	text-align: center;
	color: #333;
	margin-bottom: 60rpx;
	padding: 20rpx 0;
  }
  </style>