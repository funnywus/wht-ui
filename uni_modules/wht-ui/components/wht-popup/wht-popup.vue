<template>
  <view v-if="showPopup" class="wht-popup-mask" :class="[maskClass]" @click="handleMaskClick" :style="maskStyle">
    <view class="wht-popup-content" 
    :class="[position, customClass, { show: showContent }]" 
          :style="contentStyle"
          @click.stop>
      <text v-if="clearable" class="wht-popup-close" @click="handleClose">×</text>
      <slot></slot>
    </view>
  </view>
</template>

<script>
export default {
  name: 'wht-popup',
  props: {
    // 是否显示弹窗
    show: {
      type: Boolean,
      default: false
    },
    // 弹出位置
    position: {
      type: String,
      default: 'center'
    },
    // 自定义弹窗内容的类名
    customClass: {
      type: String,
      default: ''
    },
    // 是否显示遮罩
    mask: {
      type: Boolean,
      default: true
    },
    // 自定义遮罩的类名
    maskClass: {
      type: String,
      default: ''
    },
    // 点击遮罩是否关闭
    maskClosable: {
      type: Boolean,
      default: true
    },
    // 是否显示关闭按钮
    clearable: {
      type: Boolean,
      default: true
    },
    // 自定义弹窗样式
    customStyle: {
      type: Object,
      default: () => ({})
    },
    // 自定义遮罩样式
    maskStyle: {
      type: Object,
      default: () => ({})
    },
    // 动画时长
    duration: {
      type: Number,
      default: 300
    },
    // z-index层级
    zIndex: {
      type: Number,
      default: 999
    }
  },
  
  data() {
    return {
      showPopup: false,
      showContent: false
    }
  },
  
  computed: {
    contentStyle() {
      return {
        zIndex: this.zIndex + 1,
        transition: `all ${this.duration}ms`,
        ...this.customStyle
      }
    }
  },
  
  watch: {
    show: {
      handler(newVal) {
        if (newVal) {
          this.open()
        } else {
          this.close()
        }
      },
      immediate: true
    }
  },
  
  methods: {
    open() {
      this.showPopup = true
      setTimeout(() => {
        this.showContent = true
      }, 50)
      this.$emit('open')
    },
    
    close() {
      this.showContent = false
      setTimeout(() => {
        this.showPopup = false
      }, this.duration)
      this.$emit('close')
    },
    
    handleMaskClick() {
      if (this.maskClosable) {
        this.$emit('update:show', false)
        this.$emit('close')
      }
    },
    
    handleClose() {
      this.$emit('update:show', false)
      this.$emit('close')
    }
  }
}
</script>

<style lang="scss" scoped>
.wht-popup {
  &-mask {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.5);
    z-index: 999;
    transition: all 0.3s;
  }
  
  &-content {
    position: fixed;
    background-color: #FFFFFF !important;
    border-radius: 12rpx;
    transition: all 0.3s ease-out;
    
    .wht-popup-close {
      position: absolute;
      top: 20rpx;
      right: 20rpx;
      width: 40rpx;
      height: 40rpx;
      line-height: 40rpx;
      text-align: center;
      font-size: 32rpx;
      color: #999;
      z-index: 1;
      
      &:active {
        opacity: 0.7;
      }
    }
    
    &.center {
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%) scale(0.8);
      width: 600rpx;
      min-height: 300rpx;
      padding: 30rpx;
      opacity: 0;
      
      &.show {
        transform: translate(-50%, -50%) scale(1);
        opacity: 1;
      }
    }
    
    &.top {
      top: -100%;
      left: 0;
      width: 100%;
      height: 400rpx;
      border-radius: 0 0 12rpx 12rpx;
      
      
      &.show {
        top: 0;
      }
    }
    
    &.bottom {
      bottom: -100%;
      left: 0;
      width: 100%;
      height: 400rpx;
      border-radius: 12rpx 12rpx 0 0;
      
      &.show {
        bottom: 0;
      }
    }
    
    &.left {
      top: 0;
      left: -100%;
      height: 100vh;
      width: 500rpx;
      padding: 30rpx;
      border-radius: 0 12rpx 12rpx 0;
      
      &.show {
        left: 0;
      }
    }
    
    &.right {
      top: 0;
      right: -100%;
      height: 100vh;
      width: 500rpx;
      padding: 30rpx;
      border-radius: 12rpx 0 0 12rpx;
      
      &.show {
        right: 0;
      }
    }
  }
}
</style>
