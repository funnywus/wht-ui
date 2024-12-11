<template>
	<view class="demo-container">
	  <view class="page-header">
		<text class="title">wht-search 搜索框组件</text>
		<text class="desc">一个优雅的搜索框组件，支持多端适配</text>
	  </view>
	  
	  <!-- 基础用法 -->
	  <view class="demo-card">
		<view class="card-header">
		  <text class="card-title">基础用法</text>
		  <text class="card-desc">最基础的搜索框用法</text>
		</view>
		<wht-search v-model="searchText1" placeholder="请输入关键词搜索" />
	  </view>
	  
	  <!-- 搜索按钮样式 -->
	  <view class="demo-card">
		<view class="card-header">
		  <text class="card-title">搜索按钮样式</text>
		  <text class="card-desc">支持多种搜索按钮样式</text>
		</view>
		<view class="demo-item">
		  <text class="item-label">默认样式</text>
		  <wht-search v-model="searchText2" />
		</view>
		<view class="demo-item">
		  <text class="item-label">渐变按钮</text>
		  <wht-search 
			v-model="searchText3"
			:search-btn-style="{ 
			  background: 'linear-gradient(to right, #36d1dc, #5b86e5)',
			  boxShadow: '0 4rpx 12rpx rgba(91,134,229,0.2)'
			}"
		  />
		</view>
		<view class="demo-item">
		  <text class="item-label">暗色按钮</text>
		  <wht-search 
			v-model="searchText4"
			:search-btn-style="{ 
			  background: '#333639',
			  boxShadow: '0 4rpx 12rpx rgba(0,0,0,0.1)'
			}"
		  />
		</view>
	  </view>
	  
	  <!-- 自定义样式 -->
	  <view class="demo-card">
		<view class="card-header">
		  <text class="card-title">自定义样式</text>
		  <text class="card-desc">可自定义搜索框整体样式</text>
		</view>
		<view class="demo-item">
		  <text class="item-label">圆形风格</text>
		  <wht-search
			v-model="searchText5"
			:content-style="{ 
			  borderRadius: '100rpx',
			  background: '#f0f2f5'
			}"
			:search-btn-style="{
			  borderRadius: '100rpx',
			  background: '#2979ff'
			}"
		  />
		</view>
		<view class="demo-item">
		  <text class="item-label">投影风格</text>
		  <wht-search
			v-model="searchText6"
			:content-style="{
			  background: '#fff',
			  boxShadow: '0 4rpx 16rpx rgba(0,0,0,0.08)'
			}"
			:search-btn-style="{
			  background: '#333639',
			  boxShadow: '0 4rpx 12rpx rgba(0,0,0,0.1)'
			}"
		  />
		</view>
	  </view>
	  
	  <!-- 插槽使用 -->
	  <view class="demo-card">
		<view class="card-header">
		  <text class="card-title">插槽使用</text>
		  <text class="card-desc">通过插槽自定义更多内容</text>
		</view>
		<view class="demo-item">
		  <text class="item-label">自定义左侧</text>
		  <wht-search v-model="searchText7">
			<template #left>
			  <view class="custom-left">
				<uni-icons type="list" size="20" color="#666"></uni-icons>
			  </view>
			</template>
		  </wht-search>
		</view>
		<view class="demo-item">
		  <text class="item-label">自定义按钮</text>
		  <wht-search v-model="searchText8">
			<template #search-btn>
			  <view class="custom-btn primary">
				<text>搜索</text>
			  </view>
			</template>
		  </wht-search>
		</view>
		<view class="demo-item">
		  <text class="item-label">渐变按钮</text>
		  <wht-search v-model="searchText9">
			<template #search-btn>
			  <view class="custom-btn gradient">
				<text>搜索</text>
			  </view>
			</template>
		  </wht-search>
		</view>
	  </view>
	  
	  <!-- 事件使用 -->
	  <view class="demo-card">
		<view class="card-header">
		  <text class="card-title">事件使用</text>
		  <text class="card-desc">支持多种事件回调</text>
		</view>
		<wht-search
		  v-model="searchText10"
		  @confirm="onSearch"
		  @clear="onClear"
		  @focus="onFocus"
		  @blur="onBlur"
		  @search="onSearch"
		/>
		<view class="event-log">
		  <view class="log-title">事件日志:</view>
		  <view 
			v-for="(log, index) in eventLogs" 
			:key="index"
			class="log-item"
		  >
			{{log}}
		  </view>
		</view>
	  </view>
	</view>
  </template>
  
  <script>
  export default {
	data() {
	  return {
		searchText1: '',
		searchText2: '',
		searchText3: '',
		searchText4: '',
		searchText5: '',
		searchText6: '',
		searchText7: '',
		searchText8: '',
		searchText9: '',
		searchText10: '',
		eventLogs: []
	  }
	},
	methods: {
	  addLog(msg) {
		this.eventLogs.unshift(`${new Date().toLocaleTimeString()} - ${msg}`)
		if(this.eventLogs.length > 5) {
		  this.eventLogs.pop()
		}
	  },
	  onSearch(value) {
		this.addLog(`搜索: ${value}`)
	  },
	  onClear() {
		this.addLog('清空搜索')
	  },
	  onFocus() {
		this.addLog('获得焦点')
	  },
	  onBlur() {
		this.addLog('失去焦点')
	  }
	}
  }
  </script>
  
  <style lang="scss" scoped>
  .demo-container {
	padding: 30rpx;
	background: #f8f8f8;
	min-height: 100vh;
	
	.page-header {
	  display: flex;
	  flex-direction: column;
	  align-items: center;
	  padding: 40rpx 0;
	  
	  .logo {
		width: 120rpx;
		height: 120rpx;
		margin-bottom: 20rpx;
	  }
	  
	  .title {
		font-size: 40rpx;
		font-weight: bold;
		color: #333;
		margin-bottom: 16rpx;
	  }
	  
	  .desc {
		font-size: 28rpx;
		color: #666;
	  }
	}
	
	.demo-card {
	  background: #fff;
	  border-radius: 24rpx;
	  padding: 30rpx;
	  margin-bottom: 30rpx;
	  box-shadow: 0 2rpx 12rpx rgba(0, 0, 0, 0.05);
	  
	  .card-header {
		margin-bottom: 30rpx;
		
		.card-title {
		  font-size: 32rpx;
		  font-weight: 500;
		  color: #333;
		  margin-bottom: 12rpx;
		  display: block;
		}
		
		.card-desc {
		  font-size: 26rpx;
		  color: #999;
		}
	  }
	  
	  .demo-item {
		margin-bottom: 30rpx;
		
		&:last-child {
		  margin-bottom: 0;
		}
		
		.item-label {
		  font-size: 28rpx;
		  color: #666;
		  margin-bottom: 16rpx;
		  display: block;
		}
	  }
	  
	  .custom-left {
		width: 48rpx;
		height: 48rpx;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 50%;
		transition: all 0.3s;
		
		&:active {
		  background: #f5f5f5;
		}
	  }
	  
	  .custom-btn {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		height: 48rpx;
		min-width: 80rpx;
		padding: 0 16rpx;
		font-size: 26rpx;
		font-weight: 500;
		border-radius: 24rpx;
		transition: all 0.3s;
		
		&.primary {
		  background: #2979ff;
		  color: #fff;
		  box-shadow: 0 2rpx 8rpx rgba(41,121,255,0.15);
		}
		
		&.gradient {
		  background: linear-gradient(to right, #36d1dc, #5b86e5);
		  color: #fff;
		  box-shadow: 0 2rpx 8rpx rgba(91,134,229,0.15);
		}
		
		&:active {
		  transform: scale(0.95);
		  opacity: 0.9;
		}
	  }
	  
	  .event-log {
		margin-top: 30rpx;
		padding: 20rpx;
		background: #f5f7fa;
		border-radius: 12rpx;
		
		.log-title {
		  font-size: 28rpx;
		  color: #666;
		  margin-bottom: 16rpx;
		}
		
		.log-item {
		  font-size: 26rpx;
		  color: #999;
		  line-height: 1.8;
		}
	  }
	}
  }
  </style>