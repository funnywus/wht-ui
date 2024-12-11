<template>
	<view class="container">
	  <view class="header">
		<text class="title">图片上传组件示例</text>
		<text class="subtitle">WHT-IMG-UPLOAD</text>
	  </view>
  
	  <!-- 基础用法 -->
	  <view class="card">
		<view class="card-header">
		  <text class="card-title">基础用法</text>
		  <text class="card-desc">默认多图上传模式，最多9张</text>
		</view>
		<view class="card-body">
		  <wht-img-upload v-model="baseImages" />
		</view>
	  </view>
  
	  <!-- 回显示例 -->
	  <view class="card">
		<view class="card-header">
		  <text class="card-title">默认图片回显</text>
		  <text class="card-desc">支持默认图片展示，适用于编辑场景</text>
		</view>
		<view class="card-body">
		  <wht-img-upload v-model="defaultImages" :max="6" :columns="3" :gap="16" />
		</view>
	  </view>
  
	  <!-- 单图模式 -->
	  <view class="card">
		<view class="card-header">
		  <text class="card-title">单图模式</text>
		  <text class="card-desc">适用于头像、封面图等场景</text>
		</view>
		<view class="card-body">
		  <wht-img-upload v-model="singleImage" mode="single" :max="1" :item-height="300" button-text="上传图片" />
		</view>
	  </view>
  
	  <!-- 自定义列数 -->
	  <view class="card">
		<view class="card-header">
		  <text class="card-title">自定义列数</text>
		  <text class="card-desc">2列布局，最多4张图片</text>
		</view>
		<view class="card-body">
		  <wht-img-upload v-model="columnImages" :columns="2" :max="4" :gap="20" />
		</view>
	  </view>
  
	  <!-- 自定义样��� -->
	  <view class="card">
		<view class="card-header">
		  <text class="card-title">自定义样式</text>
		  <text class="card-desc">自定义间距和按钮文字</text>
		</view>
		<view class="card-body">
		  <wht-img-upload v-model="customImages" :columns="3" :max="6" :gap="16" button-text="添加照片"
			:show-button-text="true" />
		</view>
	  </view>
  
	  <!-- 上传配置 -->
	  <view class="card">
		<view class="card-header">
		  <text class="card-title">上传配置</text>
		  <text class="card-desc">自定义上传参数和请求头</text>
		</view>
		<view class="card-body">
		  <wht-img-upload v-model="uploadImages" :max="6" :upload-config="uploadConfig" />
		</view>
	  </view>
	</view>
  </template>
  
  <script>
  export default {
	data() {
	  return {
		defaultImages: [
		  'https://picsum.photos/300/300?random=1',
		  'https://picsum.photos/300/300?random=2',
		  'https://picsum.photos/300/300?random=3'
		],
		baseImages: [],
		singleImage: [],
		columnImages: [],
		customImages: [],
		uploadImages: [],
		uploadConfig: {
		  url: 'http://127.0.0.1:8088/common/upload',
		  name: 'file',
		  header: {
			'Authorization': 'Bearer your-token'
		  },
		  formData: {
			type: 'image',
			module: 'demo'
		  },
		  enabled: true
		}
	  }
	},
	methods: {
	  resetImages() {
		this.defaultImages = [
		  'https://picsum.photos/300/300?random=1',
		  'https://picsum.photos/300/300?random=2',
		  'https://picsum.photos/300/300?random=3'
		]
	  }
	}
  }
  </script>
  
  <style lang="scss" scoped>
  .container {
	min-height: 100vh;
	background-color: #f6f7fb;
	padding: 30rpx;
  }
  
  .header {
	text-align: center;
	padding: 40rpx 0;
	margin-bottom: 30rpx;
  
	.title {
	  font-size: 40rpx;
	  font-weight: 600;
	  color: #333;
	  display: block;
	}
  
	.subtitle {
	  font-size: 28rpx;
	  color: #666;
	  margin-top: 16rpx;
	  display: block;
	  letter-spacing: 2rpx;
	}
  }
  
  .card {
	background: #ffffff;
	border-radius: 20rpx;
	padding: 30rpx;
	margin-bottom: 30rpx;
	box-shadow: 0 4rpx 20rpx rgba(0, 0, 0, 0.05);
	transition: all 0.3s ease;
  
	&:hover {
	  transform: translateY(-2rpx);
	  box-shadow: 0 8rpx 30rpx rgba(0, 0, 0, 0.08);
	}
  
	.card-header {
	  margin-bottom: 30rpx;
  
	  .card-title {
		font-size: 32rpx;
		font-weight: 600;
		color: #333;
		display: block;
		margin-bottom: 8rpx;
	  }
  
	  .card-desc {
		font-size: 26rpx;
		color: #999;
		display: block;
	  }
	}
  
	.card-body {
	  background: #fafafa;
	  border-radius: 12rpx;
	  padding: 20rpx;
	}
  
	.card-footer {
	  margin-top: 20rpx;
	  display: flex;
	  justify-content: center;
	}
  
	.reset-btn {
	  background: #4080ff;
	  color: #fff;
	  font-size: 28rpx;
	  padding: 16rpx 40rpx;
	  border-radius: 8rpx;
	  border: none;
	  transition: all 0.3s ease;
  
	  &:active {
		background: #3070e0;
		transform: scale(0.98);
	  }
	}
  }
  
  // 适配暗黑模式
  @media (prefers-color-scheme: dark) {
	.container {
	  background-color: #1a1a1a;
	}
  
	.card {
	  background: #2a2a2a;
	  box-shadow: 0 4rpx 20rpx rgba(0, 0, 0, 0.2);
  
	  &:hover {
		box-shadow: 0 8rpx 30rpx rgba(0, 0, 0, 0.3);
	  }
  
	  .card-header {
		.card-title {
		  color: #fff;
		}
  
		.card-desc {
		  color: #888;
		}
	  }
  
	  .card-body {
		background: #333;
	  }
  
	  .reset-btn {
		background: #4080ff;
  
		&:active {
		  background: #3070e0;
		}
	  }
	}
  
	.header {
	  .title {
		color: #fff;
	  }
  
	  .subtitle {
		color: #888;
	  }
	}
  }
  </style>
  