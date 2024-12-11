<template>
  <view class="container">
    <view class="header">
      <text class="title">WHT UI</text>
      <text class="subtitle">一个轻量、可靠的移动端组件库</text>
    </view>
    
    <view class="grid">
      <view 
        class="grid-item" 
        v-for="(item, index) in list" 
        :key="index"
        @tap="goDemo(item)"
      >
        <view class="item-left">
          <view class="item-icon" :style="{ background: item.color }">
            <uni-icons :type="item.icon" size="24" color="#fff"/>
          </view>
          <view class="item-content">
            <text class="item-title">{{ item.title }}</text>
            <text class="item-desc">{{ item.desc }}</text>
          </view>
        </view>
        <uni-icons type="right" size="16" color="#ccc"/>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      list: [
        { 
          title: 'Button 按钮', 
          desc: '按钮用于触发一个操作', 
          path: '/pages/demo/button/index',
          icon: 'hand-up',
          color: '#409eff'
        },
    
        { 
          title: 'Input 输入框', 
          desc: '文本输入框', 
          path: '/pages/demo/input/index',
          icon: 'compose',
          color: '#909399'
        },
        { 
          title: 'Popup 弹出层', 
          desc: '弹出层容器', 
          path: '/pages/demo/popup/index',
          icon: 'download',
          color: '#1abc9c'
        },
        { 
          title: 'Tabs 标签页', 
          desc: '选项卡切换组件', 
          path: '/pages/demo/tabs/index',
          icon: 'list',
          color: '#d35400'
        },
        { 
          title: 'Search 搜索', 
          desc: '用于搜索场景的输入框组件', 
          path: '/pages/demo/search/index',
          icon: 'search',
          color: '#e74c3c'
        },
        { 
          title: 'Select 选择器', 
          desc: '下拉选择器', 
          path: '/pages/demo/select/index',
          icon: 'pulldown',
          color: '#34495e'
        },
        { 
          title: 'Picker 选择器', 
          desc: '通用选择器', 
          path: '/pages/demo/picker/index',
          icon: 'more',
          color: '#00d2d3'
        },
        { 
          title: 'DatetimePicker 时间选择器', 
          desc: '选择日期或时间', 
          path: '/pages/demo/datetime-picker/index',
          icon: 'calendar',
          color: '#e6a23c'
        },
        { 
          title: 'Radio 单选框', 
          desc: '在一组备选项中进行单选', 
          path: '/pages/demo/radio/index',
          icon: 'checkbox-filled',
          color: '#3498db'
        },
        { 
          title: 'Checkbox 复选框', 
          desc: '在一组备选项中进行多选', 
          path: '/pages/demo/checkbox/index',
          icon: 'checkbox',
          color: '#67c23a'
        },
        { 
          title: 'Rate 评分', 
          desc: '用于对事物进行评级操作', 
          path: '/pages/demo/rate/index',
          icon: 'star-filled',
          color: '#9b59b6'
        },
        { 
          title: 'NoticeBar 通知栏', 
          desc: '滚动消息通知', 
          path: '/pages/demo/notice-bar/index',
          icon: 'notification',
          color: '#5f27cd'
        },
        { 
          title: 'ImgUpload 图片上传', 
          desc: '图片上传组件', 
          path: '/pages/demo/img-upload/index',
          icon: 'image',
          color: '#f56c6c'
        },
        { 
          title: 'Tabbar 标签栏', 
          desc: '底部导航栏', 
          path: '/pages/demo/tabbar/index',
          icon: 'grid',
          color: '#27ae60'
        },
        { 
          title: 'Lottery 抽奖', 
          desc: '抽奖组件', 
          path: '/pages/demo/lottery/index',
          icon: 'gift',
          color: '#ff9f43'
        },
        { 
          title: 'Tag 标签', 
          desc: '用于标记和分类的标签', 
          path: '/pages/demo/tag/index',
          icon: 'tag',
          color: '#ff9900'
        },
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

<style lang="scss">
.container {
  min-height: 100vh;
  padding: 30rpx;
  background: #f8f8f8;
}

.header {
  text-align: center;
  padding: 60rpx 0;
  
  .title {
    font-size: 48rpx;
    font-weight: bold;
    color: #333;
    margin-bottom: 20rpx;
    display: block;
  }
  
  .subtitle {
    font-size: 28rpx;
    color: #666;
    display: block;
    margin-bottom: 30rpx;
  }

  .platforms {
    display: flex;
    justify-content: center;
    gap: 40rpx;
    
    .platform-item {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 10rpx;
      
      text {
        font-size: 24rpx;
        color: #666;
      }
    }
  }
}

.grid {
  display: flex;
  flex-direction: column;
  gap: 20rpx;
}

.grid-item {
  background: #fff;
  border-radius: 16rpx;
  padding: 30rpx;
  display: flex;
  align-items: center;
  justify-content: space-between;
  box-shadow: 0 2rpx 12rpx rgba(0, 0, 0, 0.05);
  transition: all 0.3s;
  
  &:active {
    transform: scale(0.98);
    opacity: 0.8;
  }
}

.item-left {
  display: flex;
  align-items: center;
  flex: 1;
}

.item-icon {
  width: 80rpx;
  height: 80rpx;
  border-radius: 16rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 24rpx;
}

.item-content {
  flex: 1;
}

.item-title {
  font-size: 32rpx;
  color: #333;
  margin-bottom: 8rpx;
  display: block;
  font-weight: 500;
}

.item-desc {
  font-size: 24rpx;
  color: #999;
  display: block;
}

// Dark mode support
@media (prefers-color-scheme: dark) {
  .container {
    background: #1a1a1a;
  }
  
  .header {
    .title {
      color: #fff;
    }
    
    .subtitle {
      color: #999;
    }
    
    .platforms {
      .platform-item {
        text {
          color: #ccc;
        }
      }
    }
  }
  
  .grid-item {
    background: #2c2c2e;
    box-shadow: 0 2rpx 12rpx rgba(0, 0, 0, 0.2);
  }
  
  .item-title {
    color: #fff;
  }
  
  .item-desc {
    color: #666;
  }
}
</style>
