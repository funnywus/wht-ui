<template>
  <view class="wht-search-container" :style="defaultContainerStyle">
    <view class="search-content" :style="defaultContentStyle">
      <!-- 左侧插槽 -->
      <slot name="left">
        <view class="default-left" :style="defaultLeftIconStyle">
          <uni-icons :type="searchIcon" :size="iconSize" :color="iconColor"></uni-icons>
        </view>
      </slot>
      
      <input
        class="search-input"
        :value="modelValue"
        :placeholder="placeholder"
        :placeholder-style="placeholderStyle"
        :focus="autoFocus"
        :maxlength="maxLength"
        :style="defaultInputStyle"
        @input="onInput"
        @confirm="onConfirm"
        @focus="onFocus"
        @blur="onBlur"
      />
      
      <!-- 清除按钮 -->
      <view 
        v-if="modelValue && showClear" 
        class="clear-icon" 
        :style="defaultClearIconStyle"
        @tap="clearInput"
      >
        <uni-icons :type="clearIcon" :size="clearIconSize" :color="clearIconColor"></uni-icons>
      </view>
      
      <!-- 搜索按钮插槽 -->
      <slot name="search-btn">
        <view 
          v-if="showSearchBtn" 
          class="search-btn"
          :style="defaultSearchBtnStyle"
          @tap="onSearch"
        >
          <text>{{searchText}}</text>
        </view>
      </slot>
    </view>
  </view>
</template>

<script>
export default {
  name: 'wht-search',
  props: {
    // 基础属性
    modelValue: { type: String, default: '' },
    placeholder: { type: String, default: '请输入关键词搜索' },
    autoFocus: { type: Boolean, default: false },
    maxLength: { type: Number, default: -1 },
    
    // 显示控制
    showClear: { type: Boolean, default: true },
    showSearchBtn: { type: Boolean, default: true },
    showDivider: { type: Boolean, default: true },
    searchText: { type: String, default: '搜索' },
    
    // 颜色配置
    bgColor: { type: String, default: '#ffffff' },
    inputBgColor: { type: String, default: '#f7f8fa' },
    textColor: { type: String, default: '#333333' },
    placeholderColor: { type: String, default: '#999999' },
    btnTextColor: { type: String, default: '#2979ff' },
    dividerColor: { type: String, default: '#e1e4e8' },
    
    // 尺寸配置
    height: { type: Number, default: 72 },
    radius: { type: Number, default: 32 },
    fontSize: { type: Number, default: 28 },
    
    // 图标配置
    searchIcon: { type: String, default: 'search' },
    clearIcon: { type: String, default: 'clear' },
    iconSize: { type: Number, default: 18 },
    clearIconSize: { type: Number, default: 14 },
    iconColor: { type: String, default: '#666666' },
    clearIconColor: { type: String, default: '#999999' },
    
    // 样式对象
    containerStyle: {
      type: Object,
      default: () => ({
        padding: '20rpx 32rpx'
      })
    },
    contentStyle: {
      type: Object,
      default: () => ({
        background: '#f7f8fa',
        borderRadius: '16rpx',
        padding: '0 20rpx',
        height: '72rpx'
      })
    },
    inputStyle: {
      type: Object,
      default: () => ({})
    },
    leftIconStyle: {
      type: Object,
      default: () => ({
        width: '48rpx',
        height: '48rpx'
      })
    },
    clearIconStyle: {
      type: Object,
      default: () => ({
        background: '#ebedf0',
        borderRadius: '50%'
      })
    },
    dividerStyle: {
      type: Object,
      default: () => ({
        height: '28rpx'
      })
    },
    searchBtnStyle: {
      type: Object,
      default: () => ({
        background: '#2979ff',
        color: '#ffffff',
        padding: '0 16rpx',
        borderRadius: '24rpx',
        fontSize: '26rpx',
        fontWeight: '500',
        marginLeft: '12rpx'
      })
    }
  },
  
  computed: {
    placeholderStyle() {
      return `color: ${this.placeholderColor}`
    },
    defaultContainerStyle() {
      return {
        padding: '20rpx 32rpx',
        ...this.containerStyle
      }
    },
    defaultContentStyle() {
      return {
        background: this.inputBgColor,
        borderRadius: `${this.radius}rpx`,
        height: `${this.height}rpx`,
        padding: '0 20rpx',
        display: 'flex',
        alignItems: 'center',
        ...this.contentStyle
      }
    },
    defaultInputStyle() {
      return {
        fontSize: `${this.fontSize}rpx`,
        color: this.textColor,
        ...this.inputStyle
      }
    },
    defaultLeftIconStyle() {
      return {
        width: '48rpx',
        height: '48rpx',
        ...this.leftIconStyle
      }
    },
    defaultClearIconStyle() {
      return {
        background: '#ebedf0',
        borderRadius: '50%',
        ...this.clearIconStyle
      }
    },
    defaultDividerStyle() {
      return {
        height: '28rpx',
        background: this.dividerColor,
        ...this.dividerStyle
      }
    },
    defaultSearchBtnStyle() {
      return {
        background: '#2979ff',
        color: '#ffffff',
        padding: '0 16rpx',
        borderRadius: '24rpx',
        fontSize: '26rpx',
        fontWeight: '500',
        marginLeft: '12rpx',
        ...this.searchBtnStyle
      }
    }
  },
  
  emits: ['update:modelValue', 'confirm', 'clear', 'focus', 'blur', 'search'],
  
  methods: {
    onInput(e) {
      this.$emit('update:modelValue', e.detail.value)
    },
    onConfirm(e) {
      this.$emit('confirm', e.detail.value)
    },
    clearInput() {
      this.$emit('update:modelValue', '')
      this.$emit('clear')
    },
    onFocus(e) {
      this.$emit('focus', e)
    },
    onBlur(e) {
      this.$emit('blur', e)
    },
    onSearch() {
      this.$emit('search', this.modelValue)
    }
  }
}
</script>

<style lang="scss" scoped>
.wht-search-container {
  .search-content {
    display: flex;
    align-items: center;
    transition: all 0.3s;
    border: 2rpx solid transparent;
    
    &:hover {
      background: v-bind('inputBgColor + "dd"');
    }
    
    &:focus-within {
      background: #ffffff;
      border-color: v-bind('dividerColor');
    }
    
    .default-left {
      display: flex;
      align-items: center;
      justify-content: center;
      transition: all 0.3s;
      opacity: 0.8;
      margin-right: 16rpx;
      
      &:active {
        opacity: 0.5;
      }
    }
    
    .search-input {
      flex: 1;
      height: 100%;
    }
    
    .clear-icon {
      width: 40rpx;
      height: 40rpx;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 16rpx;
      transition: all 0.3s;
      
      &:active {
        opacity: 0.7;
      }
    }
    
    .search-btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      height: 48rpx;
      min-width: 80rpx;
      transition: all 0.3s;
      box-shadow: 0 2rpx 8rpx rgba(41,121,255,0.15);
      
      &:active {
        transform: scale(0.95);
        opacity: 0.9;
      }
    }
  }
}
</style>
