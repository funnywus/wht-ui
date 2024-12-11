<template>
  <view class="datetime-picker">
    <view class="datetime-picker__mask" v-if="visible" @click="handleCancel"></view>
    <view class="datetime-picker__container" :class="{'datetime-picker__container--show': visible}">
      <view class="datetime-picker__header">
        <text class="datetime-picker__btn" @click="handleCancel">取消</text>
        <text class="datetime-picker__title">{{ displayTitle }}</text>
        <text class="datetime-picker__btn datetime-picker__btn--confirm" @click="handleConfirm">确定</text>
      </view>
      
      <!-- 快捷选项 -->
      <view v-if="quickOptions.length > 0" class="datetime-picker__quick">
        <text 
          v-for="(option, index) in quickOptions" 
          :key="index"
          class="datetime-picker__quick-item"
          :class="{'datetime-picker__quick-item--active': currentQuickIndex === index}"
          @click="handleQuickSelect(option, index)"
        >{{ option.label }}</text>
      </view>
      
      <!-- 区间选择标签 -->
      <view v-if="isRange" class="datetime-picker__range-tabs">
        <text 
          class="datetime-picker__range-tab"
          :class="{'datetime-picker__range-tab--active': rangeIndex === 0}"
          @click="handleRangeChange(0)"
        >开始时间</text>
        <text 
          class="datetime-picker__range-tab"
          :class="{'datetime-picker__range-tab--active': rangeIndex === 1}"
          @click="handleRangeChange(1)"
        >结束时间</text>
      </view>
      
      <view class="datetime-picker__body">
        <picker-view 
          :value="pickerValue" 
          @change="handleChange" 
          class="datetime-picker__picker"
          :indicator-style="indicatorStyle"
          :mask-style="maskStyle"
          :style="{ height: `${height}px` }"
        >
          <picker-view-column v-if="showYear">
            <view 
              class="datetime-picker__item"
              v-for="year in years" 
              :key="year"
            >{{year}}年</view>
          </picker-view-column>
          <picker-view-column v-if="showMonth">
            <view 
              class="datetime-picker__item"
              v-for="month in months" 
              :key="month"
            >{{month}}月</view>
          </picker-view-column>
          <picker-view-column v-if="showDay">
            <view 
              class="datetime-picker__item"
              v-for="day in days" 
              :key="day"
            >{{day}}日</view>
          </picker-view-column>
          <picker-view-column v-if="showHour">
            <view 
              class="datetime-picker__item"
              v-for="hour in hours" 
              :key="hour"
            >{{hour}}时</view>
          </picker-view-column>
          <picker-view-column v-if="showMinute">
            <view 
              class="datetime-picker__item"
              v-for="minute in minutes" 
              :key="minute"
            >{{minute}}分</view>
          </picker-view-column>
          <picker-view-column v-if="showSecond">
            <view 
              class="datetime-picker__item"
              v-for="second in seconds" 
              :key="second"
            >{{second}}秒</view>
          </picker-view-column>
        </picker-view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  name: 'wht-datetime-picker',
  props: {
    value: {
      type: [Date, Array, String, Number],
      default: null
    },
    mode: {
      type: String,
      default: 'datetime',
      validator: function(value) {
        return [
          'datetime', 'date', 'time', 'year', 'year-month', 'month', 'day',
          'hour-minute', 'hour-minute-second',
          'datetime-range', 'date-range', 'time-range'
        ].includes(value)
      }
    },
    title: {
      type: String,
      default: '选择时间'
    },
    showSeconds: {
      type: Boolean,
      default: false
    },
    startYear: {
      type: Number,
      default: () => new Date().getFullYear() - 5
    },
    endYear: {
      type: Number,
      default: () => new Date().getFullYear() + 5
    },
    quickOptions: {
      type: Array,
      default: () => [],
      validator: function(value) {
        return value.every(option => {
          if (!option.label) return false
          if (option.value === undefined) return false
          return true
        })
      }
    },
    height: {
      type: Number,
      default: () => 44 * 6 // 4个选项 * 44px
    }
  },
  data() {
    const now = new Date()
    return {
      visible: false,
      currentDate: now,
      rangeValues: [now, now],
      rangeIndex: 0,
      currentValue: [],
      pickerValue: [],
      currentQuickIndex: -1,
      years: [],
      months: [],
      days: [],
      hours: [],
      minutes: [],
      seconds: [],
      isInitialized: false
    }
  },
  computed: {
    isRange() {
      return this.mode.includes('range')
    },
    showYear() {
      return !['time', 'hour-minute', 'hour-minute-second'].includes(this.mode)
    },
    showMonth() {
      return ['datetime', 'date', 'year-month', 'month'].includes(this.mode) || 
             ['datetime-range', 'date-range'].includes(this.mode)
    },
    showDay() {
      return ['datetime', 'date'].includes(this.mode) || 
             ['datetime-range', 'date-range'].includes(this.mode)
    },
    showHour() {
      return ['datetime', 'time', 'hour-minute', 'hour-minute-second'].includes(this.mode) || 
             ['datetime-range', 'time-range'].includes(this.mode)
    },
    showMinute() {
      return ['datetime', 'time', 'hour-minute', 'hour-minute-second'].includes(this.mode) || 
             ['datetime-range', 'time-range'].includes(this.mode)
    },
    showSecond() {
      return (this.showSeconds && ['datetime', 'time', 'hour-minute-second'].includes(this.mode)) || 
             (this.showSeconds && ['datetime-range', 'time-range'].includes(this.mode))
    },
    columns() {
      const columns = []
      if (this.showYear) columns.push(this.years)
      if (this.showMonth) columns.push(this.months)
      if (this.showDay) columns.push(this.days)
      if (this.showHour) columns.push(this.hours)
      if (this.showMinute) columns.push(this.minutes)
      if (this.showSecond) columns.push(this.seconds)
      return columns
    },
    indicatorStyle() {
      return 'height: 44px; border-top: 1px solid #eee; border-bottom: 1px solid #eee;'
    },
    maskStyle() {
      return 'background-image: linear-gradient(180deg, rgba(255,255,255,0.95), rgba(255,255,255,0.6)), linear-gradient(0deg, rgba(255,255,255,0.95), rgba(255,255,255,0.6));'
    },
    displayTitle() {
      if (this.title !== '选择时间') return this.title
      
      const modeMap = {
        'datetime': '选择日期时间',
        'date': '选择日期',
        'time': '选择时间',
        'year': '选择年份',
        'year-month': '选择年月',
        'month': '选择月份',
        'day': '选择日期',
        'hour-minute': '选择时间',
        'hour-minute-second': '选择时间',
        'datetime-range': '选择日期时间范围',
        'date-range': '选择日期范围',
        'time-range': '选择时间范围'
      }
      
      return modeMap[this.mode] || '选择时间'
    }
  },
  watch: {
    value: {
      immediate: true,
      handler(val) {
        if (!this.visible) {
          if (this.isRange) {
            this.rangeValues = Array.isArray(val) ? val.map(v => this.parseDate(v)) : [new Date(), new Date()]
          } else {
            this.currentDate = this.parseDate(val)
          }
          this.$nextTick(() => {
            this.initData()
            this.updateCurrentValue()
          })
        }
      }
    },
    mode: {
      immediate: true,
      handler() {
        this.$nextTick(() => {
          this.initData()
          this.updateCurrentValue()
        })
      }
    },
    currentValue: {
      handler(val) {
        if (!Array.isArray(val) || val.some(v => typeof v !== 'number')) {
          console.warn('Invalid currentValue:', val)
          return
        }
        this.updateDateFromValue()
      },
      deep: true
    }
  },
  methods: {
    // 格式化日期
    formatDate(date, type = 'datetime') {
      if (!date) return ''
      
      try {
        // 确保是 Date 对象
        const d = date instanceof Date ? date : new Date(date)
        if (!this.validateDate(d)) return ''
        
        const year = d.getFullYear()
        const month = String(d.getMonth() + 1).padStart(2, '0')
        const day = String(d.getDate()).padStart(2, '0')
        const hour = String(d.getHours()).padStart(2, '0')
        const minute = String(d.getMinutes()).padStart(2, '0')
        const second = String(d.getSeconds()).padStart(2, '0')
        
        switch (type) {
          case 'datetime':
            return `${year}-${month}-${day} ${hour}:${minute}${this.showSeconds ? ':' + second : ''}`
          case 'date':
            return `${year}-${month}-${day}`
          case 'time':
            return `${hour}:${minute}${this.showSeconds ? ':' + second : ''}`
          case 'year':
            return `${year}`
          case 'year-month':
            return `${year}-${month}`
          case 'month':
            return month
          case 'day':
            return day
          case 'hour-minute':
            return `${hour}:${minute}`
          case 'hour-minute-second':
            return `${hour}:${minute}:${second}`
          default:
            return `${year}-${month}-${day} ${hour}:${minute}${this.showSeconds ? ':' + second : ''}`
        }
      } catch (error) {
        console.error('Format date error:', error, date)
        return ''
      }
    },
    
    // 解析日期
    parseDate(value) {
      if (!value) return new Date()
      
      try {
        let date
        if (value instanceof Date) {
          date = new Date(value.getTime())
        } else if (typeof value === 'number' && !isNaN(value)) {
          date = new Date(value)
        } else if (typeof value === 'string') {
          if (value.includes('T')) {
            date = new Date(value)
          } else if (value.includes('-') || value.includes('/')) {
            const parts = value.split(/[-\s:/]/).map(p => parseInt(p))
            if (parts.length >= 3) {
              date = new Date(
                parts[0], // year
                parts[1] - 1, // month
                parts[2], // day
                parts[3] || 0, // hour
                parts[4] || 0, // minute
                parts[5] || 0 // second
              )
            }
          } else {
            const timestamp = parseInt(value)
            if (!isNaN(timestamp)) {
              date = new Date(timestamp)
            }
          }
        }
        
        return date && !isNaN(date.getTime()) ? date : new Date()
      } catch (error) {
        console.error('Parse date error:', error)
        return new Date()
      }
    },
    
    show(value) {
      this.visible = true
      this.currentQuickIndex = -1
      this.rangeIndex = 0
      
      try {
        if (this.isRange) {
          // 处理区间值
          if (Array.isArray(value) && value.length === 2) {
            this.rangeValues = value.map(v => this.parseDate(v))
          } else if (typeof value === 'string') {
            // 尝试解析字符串格式的日期
            const date = this.parseDate(value)
            this.rangeValues = [date, date]
          } else {
            const now = new Date()
            this.rangeValues = [now, now]
          }
        } else {
          // 处理单个值
          this.currentDate = this.parseDate(value)
        }
        
        this.$nextTick(() => {
          this.initData()
          this.updateCurrentValue()
        })
      } catch (error) {
        console.error('Show picker error:', error)
        const now = new Date()
        if (this.isRange) {
          this.rangeValues = [now, now]
        } else {
          this.currentDate = now
        }
      }
    },
    
    hide() {
      this.visible = false
    },
    
    handleCancel() {
      this.hide()
      this.$emit('cancel')
    },
    
    handleConfirm() {
      try {
        if (this.isRange) {
          if (!this.validateDate(this.rangeValues[0]) || !this.validateDate(this.rangeValues[1])) {
            uni.showToast({
              title: '日期格式无效',
              icon: 'none'
            })
            return
          }
          
          if (this.rangeValues[1] < this.rangeValues[0]) {
            uni.showToast({
              title: '结束时间不能早于开始时间',
              icon: 'none'
            })
            return
          }
          
          const value = this.rangeValues.map(date => new Date(date.getTime()))
          const formatted = value.map(date => this.formatDate(date, this.mode.replace('-range', '')))
          
          this.$emit('input', value)
          this.$emit('change', value)
          this.$emit('confirm', {
            value,
            formatted: formatted.join(' 至 ')
          })
        } else {
          if (!this.validateDate(this.currentDate)) {
            uni.showToast({
              title: '日期格式无效',
              icon: 'none'
            })
            return
          }
          
          const value = new Date(this.currentDate.getTime())
          const formatted = this.formatDate(value, this.mode)
          
          this.$emit('input', value)
          this.$emit('change', value)
          this.$emit('confirm', {
            value,
            formatted
          })
        }
        
        this.hide()
      } catch (error) {
        console.error('Confirm error:', error)
        uni.showToast({
          title: '操作失败',
          icon: 'none'
        })
      }
    },
    
    handleQuickSelect(option, index) {
      if (!option || !option.value) {
        console.warn('Invalid quick option:', option)
        return
      }
      
      this.currentQuickIndex = index
      this.rangeIndex = 0
      
      try {
        if (this.isRange) {
          // 处理区间值
          let rangeValue = option.value
          if (!Array.isArray(rangeValue)) {
            // 如果不是数组，尝试转换
            const date = this.parseDate(rangeValue)
            rangeValue = [date, date]
          }
          
          if (rangeValue.length !== 2) {
            console.warn('Quick option value should have 2 items for range mode:', option)
            return
          }
          
          this.rangeValues = rangeValue.map(v => this.parseDate(v))
        } else {
          // 处理单个值
          this.currentDate = this.parseDate(option.value)
        }
        
        this.$nextTick(() => {
          this.initData()
          this.updateCurrentValue()
        })
        
        if (option.autoConfirm) {
          this.handleConfirm()
        }
      } catch (error) {
        console.error('Quick select error:', error)
        uni.showToast({
          title: '快捷选项格式无效',
          icon: 'none'
        })
      }
    },
    
    handleChange(e) {
      this.currentValue = e.detail.value
      this.currentQuickIndex = -1
    },
    
    handleColumnChange() {
      this.initData()
    },
    
    handleRangeChange(index) {
      if (this.rangeIndex === index) return
      this.rangeIndex = index
      this.$nextTick(() => {
        this.updateCurrentValue()
      })
    },
    
    validateDate(date) {
      if (!(date instanceof Date) || isNaN(date.getTime())) {
        console.warn('Invalid date:', date)
        return false
      }
      
      const year = date.getFullYear()
      if (year < this.startYear || year > this.endYear) {
        console.warn('Date out of range:', date)
        return false
      }
      
      return true
    },
    
    initData() {
      if (!this.isInitialized) {
        // 年
        this.years = []
        for (let i = this.startYear; i <= this.endYear; i++) {
          this.years.push(String(i))
        }
        
        // 月
        this.months = []
        for (let i = 1; i <= 12; i++) {
          this.months.push(String(i).padStart(2, '0'))
        }
        
        // 时
        this.hours = []
        for (let i = 0; i <= 23; i++) {
          this.hours.push(String(i).padStart(2, '0'))
        }
        
        // 分
        this.minutes = []
        for (let i = 0; i <= 59; i++) {
          this.minutes.push(String(i).padStart(2, '0'))
        }
        
        // 秒
        this.seconds = []
        for (let i = 0; i <= 59; i++) {
          this.seconds.push(String(i).padStart(2, '0'))
        }
        
        this.isInitialized = true
      }
      
      // 日，需要根据年月动态计算
      const date = this.isRange ? this.rangeValues[this.rangeIndex] : this.currentDate
      const year = date.getFullYear()
      const month = date.getMonth() + 1
      const daysInMonth = new Date(year, month, 0).getDate()
      
      this.days = []
      for (let i = 1; i <= daysInMonth; i++) {
        this.days.push(String(i).padStart(2, '0'))
      }
    },
    
    updateCurrentValue() {
      const date = this.isRange ? this.rangeValues[this.rangeIndex] : this.currentDate
      if (!date || isNaN(date.getTime())) {
        console.warn('Invalid date in updateCurrentValue:', date)
        return
      }
      
      const values = []
      
      if (this.showYear) {
        const yearIndex = this.years.findIndex(y => parseInt(y) === date.getFullYear())
        values.push(yearIndex >= 0 ? yearIndex : 0)
      }
      
      if (this.showMonth) {
        const monthStr = String(date.getMonth() + 1).padStart(2, '0')
        const monthIndex = this.months.findIndex(m => m === monthStr)
        values.push(monthIndex >= 0 ? monthIndex : 0)
      }
      
      if (this.showDay) {
        const dayStr = String(date.getDate()).padStart(2, '0')
        const dayIndex = this.days.findIndex(d => d === dayStr)
        values.push(dayIndex >= 0 ? dayIndex : 0)
      }
      
      if (this.showHour) {
        const hourStr = String(date.getHours()).padStart(2, '0')
        const hourIndex = this.hours.findIndex(h => h === hourStr)
        values.push(hourIndex >= 0 ? hourIndex : 0)
      }
      
      if (this.showMinute) {
        const minuteStr = String(date.getMinutes()).padStart(2, '0')
        const minuteIndex = this.minutes.findIndex(m => m === minuteStr)
        values.push(minuteIndex >= 0 ? minuteIndex : 0)
      }
      
      if (this.showSecond) {
        const secondStr = String(date.getSeconds()).padStart(2, '0')
        const secondIndex = this.seconds.findIndex(s => s === secondStr)
        values.push(secondIndex >= 0 ? secondIndex : 0)
      }
      
      this.currentValue = values
      this.pickerValue = [...values]
    },
    
    updateDateFromValue() {
      if (!Array.isArray(this.currentValue)) return
      
      let index = 0
      let year = this.currentDate.getFullYear()
      let month = this.currentDate.getMonth()
      let day = this.currentDate.getDate()
      let hour = this.currentDate.getHours()
      let minute = this.currentDate.getMinutes()
      let second = this.currentDate.getSeconds()
      
      if (this.showYear && this.currentValue[index] !== undefined) {
        year = parseInt(this.years[this.currentValue[index]])
        index++
      }
      
      if (this.showMonth && this.currentValue[index] !== undefined) {
        month = parseInt(this.months[this.currentValue[index]]) - 1
        index++
      }
      
      if (this.showDay && this.currentValue[index] !== undefined) {
        day = parseInt(this.days[this.currentValue[index]])
        index++
      }
      
      if (this.showHour && this.currentValue[index] !== undefined) {
        hour = parseInt(this.hours[this.currentValue[index]])
        index++
      }
      
      if (this.showMinute && this.currentValue[index] !== undefined) {
        minute = parseInt(this.minutes[this.currentValue[index]])
        index++
      }
      
      if (this.showSecond && this.currentValue[index] !== undefined) {
        second = parseInt(this.seconds[this.currentValue[index]])
      }
      
      const newDate = new Date(year, month, day, hour, minute, second)
      
      if (this.isRange) {
        this.rangeValues[this.rangeIndex] = newDate
        if (this.rangeIndex === 0 && this.rangeValues[1] < newDate) {
          this.rangeValues[1] = new Date(newDate)
        }
      } else {
        this.currentDate = newDate
      }
      
      this.initData()
    }
  }
}
</script>

<style scoped>
.datetime-picker {
  position: relative;
  z-index: 999;
}

.datetime-picker__mask {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.4);
  z-index: 999;
}

.datetime-picker__container {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #fff;
  transform: translateY(100%);
  transition: transform 0.3s;
  z-index: 1000;
}

.datetime-picker__container--show {
  transform: translateY(0);
}

.datetime-picker__header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 88rpx;
  padding: 0 30rpx;
  font-size: 32rpx;
  position: relative;
}

.datetime-picker__header::after {
  content: '';
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  height: 1rpx;
  background-color: #eee;
  transform: scaleY(0.5);
}

.datetime-picker__title {
  color: #333;
  font-weight: 500;
}

.datetime-picker__btn {
  color: #999;
  padding: 20rpx;
}

.datetime-picker__btn--confirm {
  color: #576B95;
  font-weight: 500;
}

.datetime-picker__body {
  position: relative;
}

.datetime-picker__picker {
  width: 100%;
}

.datetime-picker__item {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 44px;
  overflow: hidden;
  font-size: 16px;
  color: #333;
}

.datetime-picker__quick {
  display: flex;
  flex-wrap: wrap;
  padding: 10rpx 20rpx;
  border-bottom: 1rpx solid #eee;
}

.datetime-picker__quick-item {
  padding: 6rpx 20rpx;
  margin: 6rpx;
  font-size: 24rpx;
  color: #666;
  background: #f5f5f5;
  border-radius: 6rpx;
}

.datetime-picker__quick-item--active {
  color: #fff;
  background: #007AFF;
}

.datetime-picker__range-tabs {
  display: flex;
  padding: 20rpx;
  border-bottom: 1rpx solid #eee;
}

.datetime-picker__range-tab {
  flex: 1;
  text-align: center;
  font-size: 28rpx;
  color: #666;
  padding: 10rpx 0;
}

.datetime-picker__range-tab--active {
  color: #007AFF;
  position: relative;
}

.datetime-picker__range-tab--active::after {
  content: '';
  position: absolute;
  bottom: -20rpx;
  left: 50%;
  transform: translateX(-50%);
  width: 40rpx;
  height: 4rpx;
  background: #007AFF;
}
</style>
