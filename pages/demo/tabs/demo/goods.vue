<template>
  <view class="container">
    <wht-tabs 
      v-model="active" 
      :list="tabList" 
      :fixed="true"
      @change="onChange"
    >
    </wht-tabs>
    <view class="content">
      <view class="grid">
        <view 
          class="grid-item" 
          v-for="i in 8" 
          :key="i"
        >
          <view class="grid-item__img"></view>
          <text class="grid-item__text">分类 {{i}}</text>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      active: 0,
      tabList: [
        { title: '推荐' },
        { title: '手机' },
        { title: '电脑' },
        { title: '数码' },
        { title: '家电' },
        { title: '服饰' }
      ]
    }
  },
  methods: {
    onChange(index) {
      console.log('切换到:', index)
    }
  }
}
</script>

<style>
.content {
  padding: 30rpx;
  margin-top: 88rpx;
}
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30rpx;
}
.grid-item {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.grid-item__img {
  width: 120rpx;
  height: 120rpx;
  background: #f5f5f5;
  border-radius: 60rpx;
  margin-bottom: 20rpx;
}
.grid-item__text {
  font-size: 24rpx;
  color: #333;
}
</style> 