<template>
  <view class="demo-container">
    <view class="demo-block">
      <view class="demo-title">基础用法</view>
      <view class="demo-content">
        <wht-tag>默认标签</wht-tag>
        <wht-tag type="primary">主要标签</wht-tag>
        <wht-tag type="success">成功标签</wht-tag>
        <wht-tag type="warning">警告标签</wht-tag>
        <wht-tag type="error">错误标签</wht-tag>
        <wht-tag type="info">信息标签</wht-tag>
      </view>
    </view>

    <view class="demo-block">
      <view class="demo-title">空心样式</view>
      <view class="demo-content">
        <wht-tag plain>默认标签</wht-tag>
        <wht-tag type="primary" plain>主要标签</wht-tag>
        <wht-tag type="success" plain>成功标签</wht-tag>
        <wht-tag type="warning" plain>警告标签</wht-tag>
        <wht-tag type="error" plain>错误标签</wht-tag>
      </view>
    </view>

    <view class="demo-block">
      <view class="demo-title">圆角样式</view>
      <view class="demo-content">
        <wht-tag round>默认标签</wht-tag>
        <wht-tag type="primary" round>主要标签</wht-tag>
        <wht-tag type="success" round>成功标签</wht-tag>
      </view>
    </view>

    <view class="demo-block">
      <view class="demo-title">标记样式</view>
      <view class="demo-content">
        <wht-tag mark>默认标签</wht-tag>
        <wht-tag type="primary" mark>主要标签</wht-tag>
        <wht-tag type="success" mark>成功标签</wht-tag>
      </view>
    </view>

    <view class="demo-block">
      <view class="demo-title">小尺寸</view>
      <view class="demo-content">
        <wht-tag size="mini">小标签</wht-tag>
        <wht-tag type="primary" size="mini">小标签</wht-tag>
        <wht-tag type="success" size="mini">小标签</wht-tag>
      </view>
    </view>

    <view class="demo-block">
      <view class="demo-title">可关闭</view>
      <view class="demo-content">
        <wht-tag v-for="(item, index) in closableTags" 
          :key="index"
          closeable
          @close="onClose(index)"
        >{{ item }}</wht-tag>
      </view>
    </view>

    <view class="demo-block">
      <view class="demo-title">自定义颜色</view>
      <view class="demo-content">
        <wht-tag color="#8f2cdd">紫色标签</wht-tag>
        <wht-tag color="#8f2cdd" plain>紫色空心</wht-tag>
        <wht-tag gradient="linear-gradient(45deg, #f43f3b, #ec008c)">渐变标签</wht-tag>
      </view>
    </view>

    <view class="demo-block">
      <view class="demo-title">禁用状态</view>
      <view class="demo-content">
        <wht-tag disabled>禁用标签</wht-tag>
        <wht-tag type="primary" disabled>禁用标签</wht-tag>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      closableTags: ['标签1', '标签2', '标签3']
    }
  },
  methods: {
    onClose(index) {
      this.closableTags.splice(index, 1)
    }
  }
}
</script>

<style lang="scss" scoped>
.demo-container {
  padding: 20rpx;
}

.demo-block {
  margin-bottom: 30rpx;
}

.demo-title {
  margin-bottom: 20rpx;
  font-size: 28rpx;
  color: #666;
}

.demo-content {
  display: flex;
  flex-wrap: wrap;
  gap: 20rpx;
}
</style>
