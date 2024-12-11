<template>
	<view class="demo-container">
	  <!-- 基础按钮卡片 -->
	  <view class="demo-card">
		<view class="demo-card__title">基础按钮</view>
		<view class="demo-card__content">
		  <wht-button>默认按钮</wht-button>
		  <wht-button type="primary">主要按钮</wht-button>
		  <wht-button type="success">成功按钮</wht-button>
		  <wht-button type="warning">警告按钮</wht-button>
		  <wht-button type="danger">危险按钮</wht-button>
		</view>
	  </view>
  
	  <!-- 朴素按钮卡片 -->
	  <view class="demo-card">
		<view class="demo-card__title">朴素按钮</view>
		<view class="demo-card__content">
		  <wht-button plain>朴素按钮</wht-button>
		  <wht-button type="primary" plain>主要按钮</wht-button>
		  <wht-button type="success" plain>成功按钮</wht-button>
		</view>
	  </view>
  
	  <!-- 圆角按钮卡片 -->
	  <view class="demo-card">
		<view class="demo-card__title">圆角按钮</view>
		<view class="demo-card__content">
		  <wht-button round>圆角按钮</wht-button>
		  <wht-button type="primary" round>主要按钮</wht-button>
		  <wht-button type="success" round>成功按钮</wht-button>
		</view>
	  </view>
  
	  <!-- 禁用状态卡片 -->
	  <view class="demo-card">
		<view class="demo-card__title">禁用状态</view>
		<view class="demo-card__content">
		  <wht-button disabled>禁用按钮</wht-button>
		  <wht-button type="primary" disabled>禁用按钮</wht-button>
		</view>
	  </view>
  
	  <!-- 加载状态卡片 -->
	  <view class="demo-card">
		<view class="demo-card__title">加载状态</view>
		<view class="demo-card__content">
		  <wht-button loading>加载中</wht-button>
		  <wht-button type="primary" loading>加载中</wht-button>
		</view>
	  </view>
  
	  <!-- 按钮尺寸卡片 -->
	  <view class="demo-card">
		<view class="demo-card__title">按钮尺寸</view>
		<view class="demo-card__content">
		  <wht-button size="mini" type="primary">迷你按钮</wht-button>
		  <wht-button size="small" type="primary">小型按钮</wht-button>
		  <wht-button type="primary">普通按钮</wht-button>
		  <wht-button size="large" type="primary">大型按钮</wht-button>
		</view>
	  </view>
	</view>
  </template>
  
  <script>
  export default {
	name: 'button-demo'
  }
  </script>
  
  <style lang="scss">
  .demo-container {
	padding: 30rpx;
	background-color: #f5f5f5;
	min-height: 100vh;
  }
  
  .demo-card {
	background-color: #fff;
	border-radius: 16rpx;
	padding: 30rpx;
	margin-bottom: 30rpx;
	box-shadow: 0 2rpx 12rpx rgba(0, 0, 0, 0.04);
	
	&__title {
	  font-size: 32rpx;
	  font-weight: bold;
	  color: #333;
	  margin-bottom: 30rpx;
	  padding-left: 20rpx;
	  border-left: 8rpx solid #2979ff;
	}
	
	&__content {
	  display: flex;
	  flex-wrap: wrap;
	  gap: 20rpx;
	}
  }
  </style>