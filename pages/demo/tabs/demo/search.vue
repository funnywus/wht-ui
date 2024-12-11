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
      <view class="search">
        <input 
          type="text" 
          class="search-input" 
          placeholder="请输入搜索内容"
          v-model="keyword"
        />
      </view>
      <view class="list">
        <view 
          class="item" 
          v-for="i in 10" 
          :key="i"
        >
          搜索结果 {{i}}
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
      keyword: '',
      tabList: [
        { title: '综合' },
        { title: '销量' },
        { title: '新品' },
        { title: '价格' }
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
.search {
  margin-bottom: 30rpx;
}
.search-input {
  width: 100%;
  height: 80rpx;
  background: #f5f5f5;
  border-radius: 40rpx;
  padding: 0 30rpx;
  font-size: 28rpx;
}
.item {
  padding: 30rpx;
  background: #fff;
  margin-bottom: 20rpx;
  border-radius: 12rpx;
  font-size: 28rpx;
}
</style> 