<template>
  <view class="container">
    <wht-tabs 
      v-model="active" 
      :list="tabList" 
      @change="onChange"
    >
    </wht-tabs>
    <view class="content">
      <view class="text">当前选中: {{tabList[active].title}}</view>
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
}
.text {
  font-size: 28rpx;
  color: #333;
}
</style> 