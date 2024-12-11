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
      <view 
        class="item" 
        v-for="i in 30" 
        :key="i"
      >
        {{tabList[active].title}} - {{i}}
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
        { title: '标签1' },
        { title: '标签2' },
        { title: '标签3' },
        { title: '标签4' },
        { title: '标签5' }
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
.item {
  margin-bottom: 30rpx;
  font-size: 28rpx;
  color: #333;
}
</style> 