<template>
  <view class="wht-rate">
    <view 
      class="wht-rate__item" 
      v-for="(item, index) in maxCount" 
      :key="index"
      @click="handleClick(index)"
    >
      <!-- #ifdef APP-NVUE -->
      <text 
        class="wht-rate__icon"
        :class="getIconClass(index)"
        :style="getIconStyle(index)"
      >{{ getIconText(index) }}</text>
      <!-- #endif -->
      
      <!-- #ifndef APP-NVUE -->
      <text 
        class="wht-rate__icon"
        :class="[
          index < currentValue ? 'wht-rate__icon--active' : '',
          disabled ? 'wht-rate__icon--disabled' : ''
        ]"
        :style="{
          color: index < currentValue ? activeColor : voidColor,
          fontSize: size + 'rpx'
        }"
      >{{ index < currentValue ? icon : voidIcon }}</text>
      <!-- #endif -->
    </view>
  </view>
</template>

<script>
// #ifdef VUE3
import { ref, watch } from 'vue'
// #endif

export default {
  name: 'wht-rate',
  props: {
    modelValue: {
      type: Number,
      default: 0
    },
    maxCount: {
      type: Number,
      default: 5
    },
    size: {
      type: Number,
      default: 40
    },
    icon: {
      type: String,
      default: '★'
    },
    voidIcon: {
      type: String,
      default: '☆'
    },
    activeColor: {
      type: String,
      default: '#FFB800'
    },
    voidColor: {
      type: String,
      default: '#C8C9CC'
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  
  // #ifdef VUE2
  data() {
    return {
      currentValue: this.modelValue
    }
  },
  watch: {
    modelValue: {
      handler(newVal) {
        this.currentValue = newVal
      },
      immediate: true
    }
  },
  // #endif
  
  // #ifdef VUE3
  setup(props, { emit }) {
    const currentValue = ref(props.modelValue)
    
    watch(
      () => props.modelValue,
      (newVal) => {
        currentValue.value = newVal
      }
    )
    
    return {
      currentValue
    }
  },
  // #endif
  
  methods: {
    handleClick(index) {
      if (this.disabled) return
      const value = index + 1
      
      // #ifdef VUE2
      this.currentValue = value
      this.$emit('input', value)
      // #endif
      
      // #ifdef VUE3
      this.$emit('update:modelValue', value)
      // #endif
      
      this.$emit('change', value)
    },
    
    // NVUE 平台专用方法
    getIconClass(index) {
      return [
        index < this.currentValue ? 'wht-rate__icon--active' : '',
        this.disabled ? 'wht-rate__icon--disabled' : ''
      ]
    },
    getIconStyle(index) {
      return {
        color: index < this.currentValue ? this.activeColor : this.voidColor,
        fontSize: this.size + 'rpx'
      }
    },
    getIconText(index) {
      return index < this.currentValue ? this.icon : this.voidIcon
    }
  }
}
</script>

<style>
.wht-rate {
  /* #ifndef APP-NVUE */
  display: flex;
  /* #endif */
  flex-direction: row;
  align-items: center;
}
.wht-rate__item {
  padding: 0 2px;
}
.wht-rate__icon {
  /* #ifndef APP-NVUE */
  line-height: 1;
  /* #endif */
}
.wht-rate__icon--disabled {
  /* #ifndef APP-NVUE */
  cursor: not-allowed;
  /* #endif */
  opacity: 0.5;
}
</style>