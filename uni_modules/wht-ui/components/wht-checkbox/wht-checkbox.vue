<template>
  <view class="wht-checkbox-wrap">
    <!-- 单选模式 -->
    <view 
      v-if="!isList"
      class="wht-checkbox"
      :class="{ 
        'wht-checkbox--disabled': disabled,
        'wht-checkbox--round': shape === 'round'
      }"
      @click="handleClick"
      hover-class="wht-checkbox--hover"
      :hover-stay-time="150">
      <view 
        class="wht-checkbox__icon" 
        :style="[iconStyle, customStyle]">
        <view class="wht-checkbox__inner" :class="{'wht-checkbox__inner--checked': isChecked}"></view>
      </view>
      <view 
        class="wht-checkbox__label"
        :style="{ color: isChecked ? activeColor : '' }">
        <slot>{{label}}</slot>
      </view>
    </view>
    
    <!-- 列表模式 -->
    <view v-else 
      class="wht-checkbox-list"
      :class="{'wht-checkbox-list--inline': inline}">
      <view 
        v-for="(item, index) in options" 
        :key="index"
        class="wht-checkbox-item"
        :class="{ 
          'wht-checkbox-item--disabled': item.disabled,
          'wht-checkbox-item--round': shape === 'round',
          'wht-checkbox-item--inline': inline
        }"
        hover-class="wht-checkbox-item--hover"
        :hover-stay-time="150"
        @click="() => handleListClick(item)">
        <view 
          class="wht-checkbox__icon" 
          :style="[getIconStyle(item), getCustomStyle(item)]">
          <view class="wht-checkbox__inner" :class="{'wht-checkbox__inner--checked': isItemChecked(item)}"></view>
        </view>
        <view 
          class="wht-checkbox__label"
          :style="{ color: isItemChecked(item) ? activeColor : '' }">
          {{item.label}}
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  name: 'wht-checkbox',
  props: {
    modelValue: {
      type: [Boolean, Array],
      default: false
    },
    label: {
      type: String,
      default: ''
    },
    disabled: {
      type: Boolean,
      default: false
    },
    activeColor: {
      type: String,
      default: '#1989fa'
    },
    size: {
      type: String,
      default: '40rpx'
    },
    // 列表模式配置
    isList: {
      type: Boolean,
      default: false
    },
    options: {
      type: Array,
      default: () => []
    },
    shape: {
      type: String,
      default: 'square', // square 方形 | round 圆形
      validator: value => ['square', 'round'].includes(value)
    },
    inline: {
      type: Boolean,
      default: false
    },
    labelColor: {
      type: String,
      default: ''  // 选中时文字颜色，默认跟随activeColor
    }
  },
  
  computed: {
    isChecked() {
      return this.modelValue
    },
    
    customStyle() {
      if (!this.isChecked) return {}
      return {
        borderColor: this.activeColor,
        backgroundColor: this.activeColor
      }
    },
    
    iconStyle() {
      return {
        width: this.size,
        height: this.size
      }
    }
  },
  
  methods: {
    handleClick() {
      if(this.disabled) return
      this.$emit('update:modelValue', !this.modelValue)
      this.$emit('change', !this.modelValue)
    },
    
    handleListClick(item) {
      if(item.disabled) return
      
      const value = [...this.modelValue]
      const index = value.findIndex(val => val === item.value)
      
      if(index > -1) {
        value.splice(index, 1)
      } else {
        value.push(item.value)
      }
      
      this.$emit('update:modelValue', value)
      this.$emit('change', value)
    },
    
    isItemChecked(item) {
      return this.modelValue.includes(item.value)
    },
    
    getCustomStyle(item) {
      if (!this.isItemChecked(item)) return {}
      return {
        borderColor: this.activeColor,
        backgroundColor: this.activeColor
      }
    },
    
    getIconStyle(item) {
      return {
        width: this.size,
        height: this.size
      }
    }
  }
}
</script>

<style scoped>
.wht-checkbox-wrap {
  width: 100%;
}

.wht-checkbox,
.wht-checkbox-item {
  display: flex;
  align-items: center;
  padding: 24rpx;
  border-radius: 12rpx;
  background: #fff;
  transition: all 0.2s;
}

.wht-checkbox--hover,
.wht-checkbox-item--hover {
  background-color: #f5f5f5;
}

.wht-checkbox--disabled,
.wht-checkbox-item--disabled {
  opacity: 0.4;
  cursor: not-allowed;
}

.wht-checkbox__icon {
  position: relative;
  min-width: 40rpx;
  min-height: 40rpx;
  border: 2px solid #dcdee0;
  border-radius: 8rpx;
  box-sizing: border-box;
  transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
}

.wht-checkbox--round .wht-checkbox__icon,
.wht-checkbox-item--round .wht-checkbox__icon {
  border-radius: 100%;
}

.wht-checkbox__inner {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 20rpx;
  height: 12rpx;
  border: 2px solid #fff;
  border-top: none;
  border-right: none;
  transform: translate(-50%, -60%) rotate(-45deg) scale(0);
  transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
  box-sizing: border-box;
}

.wht-checkbox__inner--checked {
  transform: translate(-50%, -60%) rotate(-45deg) scale(1);
}

.wht-checkbox__label {
  margin-left: 24rpx;
  font-size: 28rpx;
  line-height: 1.5;
  transition: color 0.2s;
}

.wht-checkbox-list {
  width: 100%;
  border-radius: 12rpx;
  overflow: hidden;
  background: #fff;
  box-shadow: 0 2rpx 12rpx rgba(0, 0, 0, 0.04);
}

.wht-checkbox-item {
  margin: 0;
  border-bottom: 1px solid #f5f5f5;
}

.wht-checkbox-item:last-child {
  border-bottom: none;
}

/* 暗黑模式适配 */
@media (prefers-color-scheme: dark) {
  .wht-checkbox,
  .wht-checkbox-item,
  .wht-checkbox-list {
    background: #1a1a1a;
  }
  
  .wht-checkbox--hover,
  .wht-checkbox-item--hover {
    background-color: #2a2a2a;
  }
  
  .wht-checkbox__label {
    color: #fff;
  }
  
  .wht-checkbox-item {
    border-bottom-color: #2a2a2a;
  }
}

/* 添加行内布局样式 */
.wht-checkbox-list--inline {
  display: flex;
  flex-wrap: wrap;
  margin-right: -30rpx;  /* 抵消最后一个item的右边距 */
}

.wht-checkbox-item--inline {
  margin-right: 30rpx;  /* item之间的间距 */
  margin-bottom: 20rpx;
  flex-shrink: 0;
  border: none;  /* 移除列表模式的边框 */
  padding: 10rpx 0;
}
</style>
