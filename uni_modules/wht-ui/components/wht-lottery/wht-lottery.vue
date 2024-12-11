<template>
  <view class="lottery-machine">
    <view class="lottery-container">
      <view v-for="(reel, index) in reels" :key="index" class="lottery-reel" :style="{ height: `${itemHeight}rpx` }">
        <view class="reel-mask"></view>
        <view class="reel-strip" :style="{
          transform: `translateY(${reel.offset}rpx)`,
          transition: reel.transition
        }">
          <template v-for="repeat in 20">
            <view v-for="(item, idx) in reel.items" :key="`${repeat}-${idx}`" class="reel-item" :style="{
              height: `${itemHeight}rpx`,
              lineHeight: `${itemHeight}rpx`
            }">
              {{ item }}
            </view>
          </template>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  name: 'wht-lottery',
  props: {
    // 列数
    columns: {
      type: Number,
      default: 4
    },
    // 每列的数据
    columnValues: {
      type: Array,
      default: () => [
        // 数字
        ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'],
        // 字母
        ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J'],
        // 颜色
        ['红', '橙', '黄', '绿', '青', '蓝', '紫'],
        // 花色
        ['♠', '♥', '♣', '♦']
      ]
    },
    // 每列的延迟时间(秒)
    columnDelay: {
      type: Number,
      default: 0.15
    },
    // 转动速度(秒)
    duration: {
      type: Number,
      default: 3.5
    },
    // 总时长(秒)
    totalDuration: {
      type: Number,
      default: 5.5
    },
    // 个格子高度
    itemHeight: {
      type: Number,
      default: 120
    },
    /**
     * 每列的初始速度配置（像素/秒）
     * @example [5000, 4000, 3000, 2000] // 分别设置每列的初始速度
     * @description 如果不指定，则所有列使用相同的速度
     */
    speedConfig: {
      type: Array,
      default: () => [5000, 4500, 4000, 3500]
    }
  },
  data() {
    return {
      reels: [],
      isSpinning: false
    }
  },
  computed: {
    itemStyle() {
      return {
        height: `${this.itemHeight}rpx`,
        lineHeight: `${this.itemHeight}rpx`
      }
    }
  },
  methods: {
    // 初始化转轮数据
    initReels() {
      this.reels = Array(this.columns).fill(null).map((_, index) => ({
        items: this.columnValues[index],
        offset: 0,
        transition: 'none'
      }))

    },

    // 开始抽奖
    start(result = '') {
      if (this.isSpinning) return
      this.isSpinning = true

      const resultArray = result ? result.split('') : []

      this.reels.forEach((reel, index) => {
        // 重置过渡效果
        reel.transition = 'none'

        // 设置初始位置
        reel.offset = 0

        // 替换 requestAnimationFrame 为 setTimeout
        setTimeout(() => {
          const delay = index * this.columnDelay
          const currentDuration = this.duration + (index * 0.3)

          // 使用更适合老虎机效果的缓动函数
          reel.transition = `transform ${currentDuration}s cubic-bezier(0.45, 0.05, 0.55, 0.95) ${delay}s`

          if (resultArray[index]) {
            const targetValue = resultArray[index]
            const targetIndex = reel.items.indexOf(targetValue)
            if (targetIndex !== -1) {
              const itemsHeight = this.itemHeight * reel.items.length
              const minRotations = 8 + index
              const finalOffset = -(targetIndex * this.itemHeight + minRotations * itemsHeight)
              reel.offset = finalOffset
            }
          }
        }, 50) // 添加一个小延迟确保过渡效果正确触发
      })

      setTimeout(() => {
        this.isSpinning = false
        this.$emit('finish', resultArray)
      }, this.totalDuration * 1000)
    }
  },
  // 添加 mounted 钩子确保组件完全挂载后初始化
  mounted() {
    this.initReels()
  },
  // 确保 props 变化时重新初始化
  watch: {
    columns: {
      immediate: true,
      handler() {
        this.initReels()
      }
    },
    columnValues: {
      immediate: true,
      handler() {
        this.initReels()
      },
      deep: true
    }
  }
}
</script>

<style scoped lang="scss">
.lottery-machine {
  width: 100%;
  padding: 30rpx;
  background: #000;
  border-radius: 24rpx;
  box-sizing: border-box;
  
  // 处理安卓兼容性
  /* #ifdef APP-ANDROID */
  transform: translateZ(0);
  /* #endif */
}

.lottery-container {
  display: flex;
  justify-content: space-between;
  padding: 28rpx;
  background: #111;
  border-radius: 16rpx;
  
  > .lottery-reel {
    margin-right: 36rpx;
    &:last-child {
      margin-right: 0;
    }
  }
  
  /* #ifdef H5 */
  &:not(:root) {
    > .lottery-reel {
      margin-right: 36rpx;
      &:last-child {
        margin-right: 0;
      }
    }
  }
  /* #endif */
}

.lottery-reel {
  flex: 1;
  background: #000;
  border-radius: 8rpx;
  overflow: hidden;
  position: relative;
  border: 2rpx solid rgba(255, 255, 255, .4);
  
  /* #ifdef APP-ANDROID */
  // 优化安卓性能
  transform: translateZ(0);
  /* #endif */
}

.reel-mask {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  pointer-events: none;
  z-index: 1;
  background: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.8) 0%,
    rgba(0, 0, 0, 0) 20%,
    rgba(0, 0, 0, 0) 80%,
    rgba(0, 0, 0, 0.8) 100%
  );
}

.reel-strip {
  position: absolute;
  left: 0;
  right: 0;
  will-change: transform;
  backface-visibility: hidden;
  transform-style: preserve-3d;
  perspective: 2000rpx;
  transform: translate3d(0, 0, 0);
  z-index: 0;
  
  /* #ifdef APP-ANDROID */
  // 优化安卓动画性能
  will-change: transform;
  /* #endif */
}

.reel-item {
  width: 100%;
  text-align: center;
  font-size: 64rpx;
  font-weight: 400;
  color: #fff;
  background: #000;
  flex-shrink: 0;
  transform: translate3d(0, 0, 0);
  -webkit-font-smoothing: antialiased;
  overflow: visible;
  opacity: 1;
  visibility: visible;
  border-radius: 8rpx;
  
  // 跨平台字体适配
  /* #ifdef H5 */
  font-family: Monaco, monospace;
  /* #endif */
  
  /* #ifdef MP */
  font-family: monospace;
  /* #endif */
  
  /* #ifdef APP-ANDROID */
  font-family: monospace;
  transform: translateZ(0);
  /* #endif */
}
</style>
