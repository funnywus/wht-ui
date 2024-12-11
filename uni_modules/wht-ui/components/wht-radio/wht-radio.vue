<template>
  <view class="wht-radio" :class="{'wht-radio-disabled': disabled}">
    <!-- 列表模式 -->
    <view v-if="type === 'list'" class="wht-radio-list">
      <view 
        v-for="(item, index) in options" 
        :key="index"
        class="wht-radio-list-item"
        :class="{'wht-radio-list-item-active': modelValue === item.value}"
        @click="handleClick(item)"
      >
        <text class="wht-radio-list-label">{{ item.label }}</text>
        <view class="wht-radio-list-radio" :class="{'wht-radio-active': modelValue === item.value}" :style="radioActiveStyle">
          <text v-if="modelValue === item.value" class="wht-radio-check">✓</text>
        </view>
      </view>
    </view>
    
    <!-- 普通模式 -->
    <view v-else class="wht-radio-normal">
      <view 
        v-for="(item, index) in options"
        :key="index" 
        class="wht-radio-normal-item"
        @click="handleClick(item)"
      >
        <view class="wht-radio-normal-radio" :class="{'wht-radio-active': modelValue === item.value}" :style="radioActiveStyle">
          <text v-if="modelValue === item.value" class="wht-radio-check">✓</text>
        </view>
        <text class="wht-radio-normal-label">{{ item.label }}</text>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  name: 'wht-radio',
  props: {
    modelValue: {
      type: [String, Number],
      default: ''
    },
    options: {
      type: Array,
      default: () => []
    },
    type: {
      type: String,
      default: 'normal' // normal/list
    },
    disabled: {
      type: Boolean,
      default: false
    },
    color: {
      type: String,
      default: '#007AFF'
    }
  },
  emits: ['update:modelValue', 'change'],
  computed: {
    radioActiveStyle() {
      return {
        '--radio-active-color': this.color
      }
    }
  },
  methods: {
    handleClick(item) {
      if(this.disabled) return
      this.$emit('update:modelValue', item.value)
      this.$emit('change', item.value)
    }
  }
}
</script>

<style lang="scss" scoped>
.wht-radio {
  &-disabled {
    opacity: 0.5;
    pointer-events: none;
  }
  
  // 列表模式样式
  &-list {
    &-item {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 30rpx;
      background: #fff;
      border-bottom: 1px solid #eee;
      
      &-active {
        .wht-radio-list-radio {
          .wht-radio-list-circle {
            transform: scale(1);
          }
        }
      }
    }
    
    &-radio {
      width: 40rpx;
      height: 40rpx;
      border-radius: 50%;
      border: 1px solid #ddd;
      background-color: #fff;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: all 0.15s ease-in-out;
      
      .wht-radio-list-circle {
        width: 24rpx;
        height: 24rpx;
        border-radius: 50%;
        transform: scale(0);
        transition: transform 0.15s ease-in-out;
      }
    }
  }
  
  // 普通模式样式
  &-normal {
    display: flex;
    flex-wrap: wrap;
    
    &-item {
      display: flex;
      align-items: center;
      margin-right: 30rpx;
      margin-bottom: 20rpx;
    }
    
    &-radio {
      width: 40rpx;
      height: 40rpx;
      border-radius: 50%;
      border: 1px solid #ddd;
      background-color: #fff;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: all 0.15s ease-in-out;
      
      .wht-radio-normal-circle {
        width: 24rpx;
        height: 24rpx;
        border-radius: 50%;
        transform: scale(0);
        transition: transform 0.15s ease-in-out;
      }
    }
    
    &-active {
      .wht-radio-normal-circle {
        transform: scale(1);
      }
    }
  }
  
  &-active {
    background-color: var(--radio-active-color) !important;
    border-color: var(--radio-active-color) !important;
  }
  
  &-check {
    font-size: 24rpx;
    line-height: 1;
    color: #fff;
  }
}
</style>