<template>
  <view 
    class="tabs-wrap" 
    :style="[
      fixed ? `top: ${getTop}px;` : '',
      { background: bgColor }
    ]"
  >
    <scroll-view 
      scroll-x 
      class="tabs-scroll"
      :scroll-left="scrollLeft"
      scroll-with-animation
      :show-scrollbar="false"
    >
      <view class="tabs-nav" :style="{ height: height + 'rpx' }">
        <view 
          v-for="(item, index) in list" 
          :key="index"
          class="tabs-item"
          :class="{ active: modelValue === index }"
          :style="[
            getItemStyle(index),
            { 
              fontSize: fontSize + 'rpx',
              padding: `0 ${padding}rpx`
            }
          ]"
          @tap="onChange(index)"
        >
          {{ item.title }}
        </view>
        <view 
          class="tabs-line"
          :style="{ 
            transform: `translateX(${lineLeft}px)`,
            width: `${lineWidth}px`,
            background: activeColor,
            height: lineHeight + 'rpx'
          }"
        ></view>
      </view>
    </scroll-view>
  </view>
</template>

<script>
export default {
  name: 'wht-tabs',
  props: {
    // 数据列表
    list: {
      type: Array,
      default: () => []
    },
    // 当前选中的索引
    modelValue: {
      type: Number,
      default: 0
    },
    // 是否固定在顶部
    fixed: {
      type: Boolean,
      default: false
    },
    // 距离顶部的距离
    top: {
      type: Number,
      default: 0
    },
    // 激活状态的颜色
    activeColor: {
      type: String,
      default: '#2979ff'
    },
    // 默认状态的颜色
    color: {
      type: String,
      default: '#666666'
    },
    // 背景颜色
    bgColor: {
      type: String,
      default: '#ffffff'
    },
    // 字体大小
    fontSize: {
      type: Number,
      default: 28
    },
    // 选项卡高度
    height: {
      type: Number,
      default: 88
    },
    // 选项左右内边距
    padding: {
      type: Number,
      default: 30
    },
    // 底部线条高度
    lineHeight: {
      type: Number,
      default: 4
    },
    // 是否加粗选中项
    bold: {
      type: Boolean,
      default: true
    },
    // 最小宽度
    minWidth: {
      type: Number,
      default: 120
    }
  },
  computed: {
    getTop() {
      const sysInfo = uni.getSystemInfoSync()
      return sysInfo.statusBarHeight + 44 + this.top
    }
  },
  data() {
    return {
      scrollLeft: 0,
      lineLeft: 0,
      lineWidth: 0,
      itemWidth: 0,
      windowWidth: 0
    }
  },
  watch: {
    modelValue: {
      handler(val) {
        this.$nextTick(() => {
          this.updateLine()
          this.updateScroll()
        })
      },
      immediate: true
    }
  },
  mounted() {
    this.windowWidth = uni.getSystemInfoSync().windowWidth
    this.init()
  },
  methods: {
    init() {
      this.$nextTick(() => {
        const query = uni.createSelectorQuery().in(this)
        query.select('.tabs-item').boundingClientRect(rect => {
          if (rect) {
            this.itemWidth = rect.width
            this.updateLine()
            this.updateScroll()
          }
        }).exec()
      })
    },
    updateLine() {
      this.lineWidth = this.itemWidth * 0.6
      this.lineLeft = this.modelValue * this.itemWidth + (this.itemWidth - this.lineWidth) / 2
    },
    updateScroll() {
      const halfWindow = this.windowWidth / 2
      const targetLeft = this.modelValue * this.itemWidth
      this.scrollLeft = targetLeft - halfWindow + this.itemWidth / 2
    },
    onChange(index) {
      this.$emit('update:modelValue', index)
      this.$emit('change', index)
    },
    getItemStyle(index) {
      const isActive = this.modelValue === index
      return {
        color: isActive ? this.activeColor : this.color,
        fontWeight: isActive && this.bold ? 'bold' : 'normal',
        minWidth: this.minWidth + 'rpx'
      }
    }
  }
}
</script>

<style>
.tabs-wrap {
  width: 100%;
  z-index: 96;
}

.tabs-wrap[style*="top"] {
  position: fixed;
  left: 0;
  right: 0;
}

.tabs-scroll {
  width: 100%;
}

.tabs-nav {
  position: relative;
  display: flex;
  white-space: nowrap;
}

.tabs-item {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0 30rpx;
  height: 100%;
  min-width: 120rpx;
  font-size: 28rpx;
  position: relative;
  flex-shrink: 0;
  transition: all 0.3s;
}

.tabs-line {
  position: absolute;
  bottom: 4rpx;
  height: 4rpx;
  border-radius: 2rpx;
  transition: all 0.3s;
}
</style>
