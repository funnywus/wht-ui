<template>
	<view class="container">
	  <view 
		class="item" 
		v-for="(item, index) in list" 
		:key="index"
		@tap="goDemo(item)"
	  >
		<text class="title">{{item.title}}</text>
		<text class="arrow">></text>
	  </view>
	</view>
  </template>
  
  <script>
  export default {
	data() {
	  return {
		list: [
		  { title: '基础用法', path: '/pages/tabs/demo/basic' },
		  { title: '吸顶用法', path: '/pages/tabs/demo/sticky' },
		  { title: '搜索列表', path: '/pages/tabs/demo/search' },
		  { title: '商品分类', path: '/pages/tabs/demo/goods' }
		]
	  }
	},
	methods: {
	  goDemo(item) {
		uni.navigateTo({
		  url: item.path
		})
	  }
	}
  }
  </script>
  
  <style>
  .container {
	padding: 20rpx;
  }
  
  .item {
	display: flex;
	align-items: center;
	justify-content: space-between;
	padding: 30rpx;
	background: #fff;
	margin-bottom: 20rpx;
	border-radius: 12rpx;
  }
  
  .title {
	font-size: 28rpx;
	color: #333;
  }
  
  .arrow {
	font-size: 28rpx;
	color: #999;
  }
  </style>