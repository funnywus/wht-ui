<template>
	<view class="demo-rate">
	  <!-- 自定义颜色 -->
	  <view class="demo-rate__item">
		<view class="demo-rate__title">自定义颜色</view>
		<wht-rate 
		  v-model="value1" 
		  active-color="#FF4444"
		  void-color="#DDDDDD"
		/>
	  </view>
	  
	  <!-- 自定义图标 -->
	  <view class="demo-rate__item">
		<view class="demo-rate__title">自定义图标</view>
		<wht-rate 
		  v-model="value2"
		  icon="❤"
		  void-icon="♡"
		  active-color="#FF6666"
		/>
	  </view>
	  
	  <!-- 半星评分 -->
	  <view class="demo-rate__item">
		<view class="demo-rate__title">半星评分</view>
		<wht-rate 
		  v-model="value3"
		  :allow-half="true"
		  active-color="#FFB800"
		/>
	  </view>
	  
	  <!-- 自定义数量 -->
	  <view class="demo-rate__item">
		<view class="demo-rate__title">自定义数量</view>
		<wht-rate 
		  v-model="value4"
		  :max="7"
		  active-color="#2196F3"
		/>
	  </view>
	  
	  <!-- 带描述文字 -->
	  <view class="demo-rate__item">
		<view class="demo-rate__title">带描述文字</view>
		<view class="demo-rate__row">
		  <wht-rate v-model="value5" />
		  <text class="demo-rate__text">{{ rateTexts[value5 - 1] || '请评分' }}</text>
		</view>
	  </view>
	  
	  <!-- 评价场景 -->
	  <view class="demo-rate__item">
		<view class="demo-rate__title">评价场景</view>
		<view class="demo-rate__comment">
		  <view class="demo-rate__label">商品评分</view>
		  <wht-rate v-model="comment.goods" :size="24" />
		</view>
		<view class="demo-rate__comment">
		  <view class="demo-rate__label">物流评分</view>
		  <wht-rate v-model="comment.delivery" :size="24" />
		</view>
		<view class="demo-rate__comment">
		  <view class="demo-rate__label">服务评分</view>
		  <wht-rate v-model="comment.service" :size="24" />
		</view>
	  </view>
	</view>
  </template>
  
  <script>
  export default {
	data() {
	  return {
		value1: 4,
		value2: 3,
		value3: 2.5,
		value4: 6,
		value5: 3,
		rateTexts: ['差评', '一般', '满意', '很好', '非常好'],
		comment: {
		  goods: 5,
		  delivery: 4,
		  service: 5
		}
	  }
	}
  }
  </script>
  
  <style>
  .demo-rate {
	padding: 30rpx;
  }
  
  .demo-rate__item {
	margin-bottom: 50rpx;
	padding: 20rpx;
	background: #fff;
	border-radius: 12rpx;
  }
  
  .demo-rate__title {
	margin-bottom: 20rpx;
	font-size: 28rpx;
	color: #333;
	font-weight: bold;
  }
  
  .demo-rate__row {
	display: flex;
	align-items: center;
  }
  
  .demo-rate__text {
	margin-left: 20rpx;
	font-size: 26rpx;
	color: #666;
  }
  
  .demo-rate__comment {
	display: flex;
	align-items: center;
	margin-bottom: 20rpx;
  }
  
  .demo-rate__label {
	width: 140rpx;
	font-size: 26rpx;
	color: #666;
  }
  
  /* 添加卡片阴影效果 */
  .demo-rate__item {
	box-shadow: 0 2rpx 12rpx rgba(0, 0, 0, 0.05);
  }
  
  /* 添加hover效果 */
  .demo-rate__item:active {
	opacity: 0.8;
  }
  </style> 