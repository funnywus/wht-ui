<template>
  <view 
    class="wht-input-wrapper" 
    :class="[type, {'is-disabled': disabled}]"
    :style="{
      borderColor: borderColor,
      backgroundColor: backgroundColor,
      borderRadius: radius + 'px'
    }"
  >
    <!-- 前置插槽 -->
    <view 
      class="prefix" 
      v-if="$slots.prefix || prefixIcon"
      :style="{ color: iconColor }"
    >
      <slot name="prefix"></slot>
      <uni-icons v-if="prefixIcon" :type="prefixIcon" size="16" :color="iconColor"></uni-icons>
    </view>
    
    <!-- 输入框主体 -->
    <input
      class="wht-input"
      :value="modelValue"
      :type="inputType"
      :password="password"
      :placeholder="placeholder"
      :disabled="disabled"
      :maxlength="maxlength"
      :focus="focus"
      :style="{
        color: textColor,
        'placeholder-color': placeholderColor
      }"
      @input="onInput"
      @focus="onFocus"
      @blur="onBlur"
      @confirm="onConfirm"
    />
    
    <!-- 后置插槽 -->
    <view 
      class="suffix" 
      v-if="$slots.suffix || suffixIcon || clearable"
      :style="{ color: iconColor }"
    >
      <uni-icons 
        v-if="clearable && modelValue" 
        type="clear" 
        size="16" 
        :color="iconColor"
        @click="clearInput"
      ></uni-icons>
      <slot name="suffix"></slot>
      <uni-icons 
        v-if="suffixIcon" 
        :type="suffixIcon" 
        size="16" 
        :color="iconColor"
      ></uni-icons>
    </view>
  </view>
</template>

<script>
export default {
  name: 'wht-input',
  props: {
    modelValue: {
      type: [String, Number],
      default: ''
    },
    type: {
      type: String,
      default: 'text'
    },
    placeholder: {
      type: String,
      default: '请输入'
    },
    disabled: {
      type: Boolean,
      default: false
    },
    clearable: {
      type: Boolean,
      default: false
    },
    maxlength: {
      type: Number,
      default: -1
    },
    prefixIcon: {
      type: String,
      default: ''
    },
    suffixIcon: {
      type: String,
      default: ''
    },
    password: {
      type: Boolean,
      default: false
    },
    focus: {
      type: Boolean,
      default: false  
    },
    borderColor: {
      type: String,
      default: '#dcdfe6'
    },
    backgroundColor: {
      type: String,
      default: '#ffffff'
    },
    textColor: {
      type: String,
      default: '#606266'
    },
    iconColor: {
      type: String,
      default: '#999'
    },
    placeholderColor: {
      type: String,
      default: '#c0c4cc'
    },
    radius: {
      type: [Number, String],
      default: 4
    }
  },
  computed: {
    inputType() {
      const typeMap = {
        text: 'text',
        password: 'password',
        number: 'number',
        idcard: 'idcard',
        digit: 'digit'
      }
      return typeMap[this.type] || 'text'
    }
  },
  methods: {
    onInput(e) {
      this.$emit('update:modelValue', e.detail.value)
      this.$emit('input', e)
    },
    onFocus(e) {
      this.$emit('focus', e)
    },
    onBlur(e) {
      this.$emit('blur', e)
    },
    onConfirm(e) {
      this.$emit('confirm', e)
    },
    clearInput() {
      this.$emit('update:modelValue', '')
      this.$emit('clear')
    }
  }
}
</script>

<style lang="scss" scoped>
.wht-input-wrapper {
  display: flex;
  align-items: center;
  width: 100%;
  min-height: 35px;
  border-width: 1px;
  border-style: solid;
  padding: 0 12px;
  box-sizing: border-box;
  transition: all 0.3s;
  
  &.search {
  }
  
  &.is-disabled {
    cursor: not-allowed;
    
    .wht-input {
      cursor: not-allowed;
    }
  }
  
  .prefix, .suffix {
    display: flex;
    align-items: center;
  }
  
  .prefix {
    margin-right: 8px;
  }
  
  .suffix {
    margin-left: 8px;
  }
  
  .wht-input {
    flex: 1;
    width: 100%;
    height: 100%;
    line-height: 35px;
    border: none;
    outline: none;
    background: none;
    font-size: 14px;
  }
}
</style>
