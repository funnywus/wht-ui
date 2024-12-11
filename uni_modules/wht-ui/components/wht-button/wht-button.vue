<template>
  <button
    class="wht-button"
    :class="[
      `wht-button--${type}`,
      `wht-button--${size}`,
      {
        'wht-button--plain': plain,
        'wht-button--round': round,
        'wht-button--disabled': disabled,
        'wht-button--loading': loading
      }
    ]"
    :disabled="disabled"
    :loading="loading"
    @click="handleClick"
  >
    <view class="wht-button__content">
      <text v-if="loading" class="wht-button__loading-icon">加载中...</text>
      <text v-else><slot></slot></text>
    </view>
  </button>
</template>

<script>
export default {
  name: 'wht-button',
  props: {
    // 按钮类型
    type: {
      type: String,
      default: 'default',
      validator: value => {
        return ['default', 'primary', 'success', 'warning', 'danger'].includes(value)
      }
    },
    // 按钮尺寸
    size: {
      type: String,
      default: 'normal',
      validator: value => {
        return ['mini', 'small', 'normal', 'large'].includes(value)
      }
    },
    // 是否朴素按钮
    plain: {
      type: Boolean,
      default: false
    },
    // 是否圆角按钮
    round: {
      type: Boolean,
      default: false
    },
    // 是否禁用
    disabled: {
      type: Boolean,
      default: false
    },
    // 是否显示加载状态
    loading: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    handleClick(e) {
      if (!this.disabled && !this.loading) {
        this.$emit('click', e)
      }
    }
  }
}
</script>

<style lang="scss">
.wht-button {
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0 30rpx;
  font-size: 28rpx;
  height: 80rpx;
  line-height: 1;
  text-align: center;
  border-radius: 8rpx;
  border: 2rpx solid transparent;
  transition: all 0.2s;
  
  // 默认样式
  background-color: #f5f5f5;
  color: #333;
  
  &--primary {
    background-color: #2979ff;
    color: #fff;
  }
  
  &--success {
    background-color: #19be6b;
    color: #fff;
  }
  
  &--warning {
    background-color: #ff9900;
    color: #fff;
  }
  
  &--danger {
    background-color: #fa3534;
    color: #fff;
  }
  
  // 尺寸
  &--mini {
    height: 50rpx;
    padding: 0 20rpx;
    font-size: 20rpx;
  }
  
  &--small {
    height: 60rpx;
    padding: 0 24rpx;
    font-size: 24rpx;
  }
  
  &--large {
    height: 100rpx;
    padding: 0 40rpx;
    font-size: 32rpx;
  }
  
  // 朴素按钮
  &--plain {
    background-color: transparent;
    
    &.wht-button--primary {
      color: #2979ff;
      border-color: #2979ff;
    }
    
    &.wht-button--success {
      color: #19be6b;
      border-color: #19be6b;
    }
    
    &.wht-button--warning {
      color: #ff9900;
      border-color: #ff9900;
    }
    
    &.wht-button--danger {
      color: #fa3534;
      border-color: #fa3534;
    }
  }
  
  // 圆角按钮
  &--round {
    border-radius: 100rpx;
  }
  
  // 禁用状态
  &--disabled {
    opacity: 0.6;
    cursor: not-allowed;
  }
  
  // 加载状态
  &--loading {
    opacity: 0.8;
    cursor: default;
  }
  
  &__content {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  &__loading-icon {
    margin-right: 10rpx;
  }
}
</style>
