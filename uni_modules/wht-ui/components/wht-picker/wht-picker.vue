<template>
  <view class="wht-picker" v-if="isVisible">
    <view class="wht-picker__mask" @tap="handleCancel"></view>
    <view class="wht-picker__container">
      <view class="wht-picker__header">
        <text class="wht-picker__cancel" @tap="handleCancel">取消</text>
        <text class="wht-picker__title">{{title}}</text>
        <text class="wht-picker__confirm" @tap="handleConfirm">确定</text>
      </view>
      <view class="wht-picker__body">
        <picker-view 
          :value="pickerValue" 
          @change="handleChange" 
          class="picker-view"
          :indicator-style="indicatorStyle || 'height: 88rpx;'"
          :mask-style="maskStyle"
        >
          <picker-view-column v-for="(column, index) in displayColumns" :key="index">
            <view 
              class="picker-item" 
              v-for="(item, i) in column" 
              :key="i"
            >
              <text>{{item[labelKey]}}</text>
            </view>
          </picker-view-column>
        </picker-view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  name: 'wht-picker',
  props: {
    modelValue: {
      type: Array,
      default: () => []
    },
    columns: {
      type: Array,
      default: () => []
    },
    title: {
      type: String,
      default: '请选择'
    },
    type: {
      type: String,
      default: 'single'
    },
    labelKey: {
      type: String,
      default: 'label'
    },
    separator: {
      type: String,
      default: '/'
    },
    indicatorStyle: {
      type: String,
      default: 'height: 88rpx; line-height: 88rpx;'
    },
    maskStyle: {
      type: String,
      default: ''
    },
    clearable: {
      type: Boolean,
      default: false
    }
  },

  data() {
    return {
      isVisible: false,
      pickerValue: [],
      displayColumns: [],
      innerValue: [],
      pendingValue: []
    }
  },

  watch: {
    modelValue: {
      handler(val) {
        if (val && val.length) {
          this.innerValue = [...val]
          this.pickerValue = [...val]
        } else {
          this.setDefaultValue()
        }
        this.updateColumns()
      },
      immediate: true
    },
    
    columns: {
      handler() {
        this.updateColumns()
      },
      immediate: true
    }
  },

  methods: {
    // 更新列数据
    updateColumns() {
      if (this.type === 'single') {
        this.displayColumns = [this.columns]
        // 确保单列选择的值在有效范围内
        const maxIndex = this.columns.length - 1
        if (this.pickerValue[0] > maxIndex) {
          this.pickerValue = [maxIndex]
        }
      } else if (this.type === 'multi') {
        this.displayColumns = this.columns
        // 确保多列选择的值在有效范围内
        this.pickerValue = this.pickerValue.map((value, index) => {
          const maxIndex = (this.columns[index] || []).length - 1
          return value > maxIndex ? maxIndex : value
        })
      } else if (this.type === 'linkage') {
        const getColumns = (data, level = 0) => {
          if (!data || !data.length) return []
          const selectedIndex = this.pickerValue[level] || 0
          const nextData = data[selectedIndex]?.children
          return [data, ...getColumns(nextData, level + 1)]
        }
        this.displayColumns = getColumns(this.columns)
      }
    },

    // 设置默认值
    setDefaultValue() {
      if (this.type === 'single') {
        // 单列选择时确保有效的默认值
        const defaultIndex = 0
        this.innerValue = [defaultIndex]
        this.pickerValue = [defaultIndex]
      } else if (this.type === 'multi') {
        // 多列选择时为每列设置默认值
        this.innerValue = this.columns.map(() => 0)
        this.pickerValue = [...this.innerValue]
      } else if (this.type === 'linkage') {
        const getDefaultValue = (data) => {
          if (!data || !data.length) return []
          return [0, ...getDefaultValue(data[0]?.children)]
        }
        this.innerValue = getDefaultValue(this.columns)
      }
      this.$emit('update:modelValue', this.innerValue)
    },

    // 获取选中项
    getSelectedItems() {
      if (this.type === 'single') {
        const index = this.pickerValue[0]
        return this.columns[index] ? [this.columns[index]] : []
      } else if (this.type === 'multi') {
        return this.pickerValue.map((index, columnIndex) => 
          this.columns[columnIndex]?.[index]
        ).filter(Boolean)
      } else if (this.type === 'linkage') {
        const getItems = (data, level = 0) => {
          if (!data || !data.length) return []
          const index = this.pickerValue[level]
          const item = data[index]
          if (!item) return []
          return [item, ...getItems(item.children, level + 1)]
        }
        return getItems(this.columns)
      }
      return []
    },

    // 打开选择器
    open() {
      this.isVisible = true
      this.pickerValue = [...this.innerValue]
      this.updateColumns()
    },
    
    // 关闭选择器
    close() {
      this.isVisible = false
    },
    
    // 设置值
    setValue(value) {
      if (!Array.isArray(value)) {
        console.warn('setValue方法参数必须是数组')
        return
      }
      
      this.innerValue = [...value]
      this.pickerValue = [...value]
      this.updateColumns()
      this.$emit('update:modelValue', this.innerValue)
    },
    
    // 获取当前值
    getValue() {
      return [...this.innerValue]
    },
    
    // 处理确认
    handleConfirm() {
      this.innerValue = [...this.pickerValue]
      const selectedItems = this.getSelectedItems()
      const displayText = selectedItems
        .map(item => item?.[this.labelKey])
        .filter(Boolean)
        .join(this.separator)
      
      this.$emit('update:modelValue', this.innerValue)
      this.$emit('confirm', {
        value: this.innerValue,
        items: selectedItems,
        display: displayText
      })
      this.close()
    },
    
    // 处理取消
    handleCancel() {
      this.$emit('cancel')
      this.close()
    },
    
    // 处理变更
    handleChange(e) {
      const newValue = e.detail.value
      if (this.type === 'single') {
        // 确保单列选择的值在有效范围内
        const maxIndex = this.columns.length - 1
        const index = Math.min(newValue[0], maxIndex)
        this.pickerValue = [index]
      } else if (this.type === 'multi') {
        // 确保多列选择的值在有效范围内
        this.pickerValue = newValue.map((value, index) => {
          const maxIndex = (this.columns[index] || []).length - 1
          return Math.min(value, maxIndex)
        })
      } else if (this.type === 'linkage') {
        this.pickerValue = [...newValue]
        this.updateColumns()
      }
      
      this.$emit('change', {
        value: this.pickerValue,
        items: this.getSelectedItems()
      })
    },
    
    // 新增：清空方法
    clear() {
      this.innerValue = []
      this.pickerValue = []
      this.$emit('update:modelValue', [])
      this.$emit('clear')
    }
  }
}
</script>

<style>
.wht-picker {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 999;
}

.wht-picker__mask {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.4);
  z-index: 999;
}

.wht-picker__container {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  background: #fff;
  transform: translateY(0);
  z-index: 1000;
}

.wht-picker__header {
  display: flex;
  align-items: center;
  padding: 20rpx 30rpx;
  background: #fff;
  position: relative;
}

.wht-picker__header::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: 0;
  right: 0;
  height: 1px;
  background: #eee;
  transform: scaleY(0.5);
}

.wht-picker__cancel,
.wht-picker__confirm {
  font-size: 32rpx;
  color: #666;
  padding: 0 20rpx;
}

.wht-picker__confirm {
  color: #007aff;
}

.wht-picker__title {
  flex: 1;
  text-align: center;
  font-size: 32rpx;
  color: #333;
}

.wht-picker__body {
  width: 100%;
  height: 480rpx;
  overflow: hidden;
  position: relative;
}

.picker-view {
  width: 100%;
  height: 100%;
}

.picker-view-column {
  flex: 1;
  width: 0;
}

.picker-item {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 32rpx;
  color: #333;
  padding: 0 12rpx;
  box-sizing: border-box;
  width: 100%;
}

.picker-item text {
  text-align: center;
  width: 100%;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Single column style */
.wht-picker__body :deep(.uni-picker-view-column:only-child) {
  width: 100%;
}

/* Multiple columns style */
.wht-picker__body :deep(.uni-picker-view-column) {
  flex: 1;
  width: 0;
}
</style>
