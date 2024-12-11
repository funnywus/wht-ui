<template>
  <view 
    class="wht-tag"
    :class="[
      `wht-tag--${type}`,
      `wht-tag--${size}`,
      {
        'wht-tag--plain': plain,
        'wht-tag--round': round,
        'wht-tag--mark': mark,
        'wht-tag--closeable': closeable,
        'wht-tag--disabled': disabled,
        'wht-tag--gradient': gradient
      }
    ]"
    :style="[
      customStyle,
      { 
        backgroundColor: gradient ? 'transparent' : (plain ? 'transparent' : color),
        background: gradient || '',
        color: gradient ? (textColor || '#fff') : (plain ? (color || getTypeColor()) : textColor || '#fff'),
        borderColor: gradient ? 'transparent' : (color || getTypeColor()),
        border: gradient ? 'none' : ''
      }
    ]"
    @click="onClick"
  >
    <slot></slot>
    <text 
      v-if="closeable" 
      class="wht-tag__close"
      @click.stop="onClose"
    >×</text>
  </view>
</template>

<script>
/**
 * tag 标签
 * @description 用于标记和分类的标签组件
 * @tutorial https://ext.dcloud.net.cn/plugin?id=xxx
 * @property {String} type = [default|primary|success|warning|error|info] 标签类型
 * @property {String} color 标签颜色
 * @property {String} gradient 渐变背景色，例如：'linear-gradient(45deg, #f43f3b, #ec008c)'
 * @property {String} text-color 文字颜色，优先级高于type
 * @property {String} size = [default|mini] 标签尺寸
 * @property {Boolean} plain = [true|false] 是否空心
 * @property {Boolean} round = [true|false] 是否圆角
 * @property {Boolean} mark = [true|false] 是否标记样式
 * @property {Boolean} closeable = [true|false] 是否可关闭
 * @property {Boolean} disabled = [true|false] 是否禁用
 * @property {Object} custom-style 自定义样式
 * @event {Function} click 点击标签触发
 * @event {Function} close 关闭标签触发
 */
export default {
  name: 'wht-tag',
  props: {
    // 标签类型
    type: {
      type: String,
      default: 'default',
      validator: function(value) {
        return ['default', 'primary', 'success', 'warning', 'error', 'info'].indexOf(value) !== -1
      }
    },
    // 标签颜色
    color: {
      type: String,
      default: ''
    },
    // 渐变背景色
    gradient: {
      type: String,
      default: ''
    },
    // 文字颜色
    textColor: {
      type: String,
      default: ''
    },
    // 标签尺寸
    size: {
      type: String,
      default: 'default',
      validator: function(value) {
        return ['default', 'mini'].indexOf(value) !== -1
      }
    },
    // 是否空心
    plain: {
      type: Boolean,
      default: false
    },
    // 是否圆角
    round: {
      type: Boolean,
      default: false
    },
    // 是否标记样式
    mark: {
      type: Boolean,
      default: false
    },
    // 是否可关闭
    closeable: {
      type: Boolean,
      default: false
    },
    // 是否禁用
    disabled: {
      type: Boolean,
      default: false
    },
    // 自定义样式
    customStyle: {
      type: Object,
      default: () => ({})
    }
  },
  emits: ['click', 'close'],
  methods: {
    onClick(e) {
      if (!this.disabled) {
        this.$emit('click', e)
      }
    },
    onClose(e) {
      this.$emit('close', e)
    },
    getTypeColor() {
      const colorMap = {
        default: '#909399',
        primary: '#2979ff',
        success: '#19be6b',
        warning: '#ff9900',
        error: '#fa3534',
        info: '#909399'
      }
      return colorMap[this.type]
    }
  }
}
</script>

<style lang="scss" scoped>
.wht-tag {
  display: inline-flex;
  align-items: center;
  padding: 0 16rpx;
  border-radius: 4rpx;
  height: 48rpx;
  font-size: 24rpx;
  line-height: 1;
  border: 2rpx solid transparent;
  position: relative;
  z-index: 0;
  
  // 尺寸
  &--mini {
    height: 32rpx;
    padding: 0 8rpx;
    font-size: 20rpx;
  }
  
  // 类型
  &--default {
    background-color: #909399;
    color: #ffffff;
  }
  &--primary {
    background-color: #2979ff;
    color: #ffffff;
  }
  &--success {
    background-color: #19be6b;
    color: #ffffff;
  }
  &--warning {
    background-color: #ff9900;
    color: #ffffff;
  }
  &--error {
    background-color: #fa3534;
    color: #ffffff;
  }
  &--info {
    background-color: #909399;
    color: #ffffff;
  }
  
  // 空心
  &--plain {
    background-color: transparent;
    
    &.wht-tag--default {
      color: #909399;
      border-color: #909399;
    }
    &.wht-tag--primary {
      color: #2979ff;
      border-color: #2979ff;
    }
    &.wht-tag--success {
      color: #19be6b;
      border-color: #19be6b;
    }
    &.wht-tag--warning {
      color: #ff9900;
      border-color: #ff9900;
    }
    &.wht-tag--error {
      color: #fa3534;
      border-color: #fa3534;
    }
    &.wht-tag--info {
      color: #909399;
      border-color: #909399;
    }
  }
  
  // 圆角
  &--round {
    border-radius: 100rpx;
  }
  
  // 标记样式
  &--mark {
    border-radius: 0 100rpx 100rpx 0;
  }
  
  // 渐变样式
  &--gradient {
    border: none;
    background: v-bind(gradient);
  }
  
  // 禁用状态
  &--disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
  
  // 关闭按钮
  &__close {
    margin-left: 8rpx;
    font-size: 24rpx;
    
    &:active {
      opacity: 0.7;
    }
  }
}
</style>
