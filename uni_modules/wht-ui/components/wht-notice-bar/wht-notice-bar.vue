<template>
    <view class="wht-notice-bar" 
          :class="[`wht-notice-bar--${type}`, { 'is-multi': !single }]"
          :style="[barStyle, { borderRadius: `${radius}rpx` }]" 
          v-if="isShow">
        <!-- 左侧图标 -->
        <view class="wht-notice-bar__left" v-if="showIcon">
            <slot name="leftIcon">
                <uni-icons :type="getIconType" :color="iconColor" size="20"></uni-icons>
            </slot>
        </view>

        <!-- 内容区域 -->
        <view class="wht-notice-bar__content">
            <!-- #ifdef MP -->
            <view class="wht-notice-bar__text" 
                  :class="[
                    single ? 'single-line' : 'multi-line',
                    { 'no-scroll': !needScroll }
                  ]"
                  :animation="animationData"
                  @tap="onClick">
                <text>{{text}}</text>
            </view>
            <!-- #endif -->
            
            <!-- #ifdef H5 || APP-PLUS -->
            <view class="wht-notice-bar__text" 
                  :class="[
                    single ? 'single-line' : 'multi-line',
                    { 'css-animation': single && isReady && needScroll },
                    { 'no-scroll': !needScroll }
                  ]"
                  :style="[
                    !single ? { '-webkit-line-clamp': rows } : null,
                    cssAnimationStyle
                  ]"
                  @tap="onClick">
                <text>{{text}}</text>
            </view>
            <!-- #endif -->
        </view>

        <!-- 右侧关闭图标 -->
        <view class="wht-notice-bar__right" v-if="showClose" @tap="onClose">
            <slot name="rightIcon">
                <uni-icons type="closeempty" :color="iconColor" size="20"></uni-icons>
            </slot>
        </view>
    </view>
</template>

<script>
const isVue3 = typeof window !== 'undefined' && window.Vue && window.Vue.version.startsWith('3')

export default {
    name: 'wht-notice-bar',
    props: {
        text: {
            type: String,
            default: '',
            desc: '通知文本内容'
        },
        type: {
            type: String,
            default: 'warning',
            validator: value => {
                return ['primary', 'success', 'warning', 'error', 'info'].includes(value)
            },
            desc: '主题类型'
        },
        bgColor: {
            type: String,
            default: '',
            desc: '背景颜色'
        },
        color: {
            type: String,
            default: '',
            desc: '文字颜色'
        },
        showIcon: {
            type: Boolean,
            default: true,
            desc: '是否显示左侧图标'
        },
        showClose: {
            type: Boolean,
            default: false,
            desc: '是否显示右侧关闭按钮'
        },
        speed: {
            type: Number,
            default: 0,
            desc: '滚动速度，单位px/s'
        },
        single: {
            type: Boolean,
            default: true,
            desc: '是否单行显示'
        },
        rows: {
            type: Number,
            default: 2,
            desc: '多行显示时的行数'
        },
        radius: {
            type: [String, Number],
            default: 12,
            desc: '圆角大小，单位rpx'
        },
        iconColor: {
            type: String,
            default: '',
            desc: '图标颜色，默认跟随文字颜色'
        },
        // 是否开启滚动
        scrollable: {
            type: Boolean,
            default: false,
            desc: '是否开启滚动'
        }
    },

    data() {
        return {
            isShow: true,
            isReady: false,
            textWidth: 0,
            containerWidth: 0,
            animation: null,
            animationData: null,
            platform: ''
        }
    },

    computed: {
        getIconType() {
            const typeMap = {
                primary: 'info',
                success: 'checkmarkempty',
                warning: 'sound',
                error: 'closeempty',
                info: 'info'
            }
            return typeMap[this.type] || 'sound'
        },
        
        barStyle() {
            const style = {}
            if (this.bgColor) {
                style.backgroundColor = this.bgColor
            }
            if (this.color) {
                style.color = this.color
            }
            return style
        },
        
        textStyle() {
            const style = {}
            if (!this.single) {
                style['-webkit-line-clamp'] = this.rows
            }
            return style
        },
        
        cssAnimationStyle() {
            if (!this.single || !this.isReady) return {}
            
            const duration = (this.textWidth + this.containerWidth) / this.speed
            return {
                '--scroll-width': `${this.textWidth}px`,
                '--container-width': `${this.containerWidth}px`,
                '--animation-duration': `${duration}s`
            }
        },
        
        // 是否需要滚动
        needScroll() {
            return this.scrollable && this.speed > 0
        }
    },

    // #ifdef VUE3
    beforeMount() {
        this.setPlatform()
    },
    // #endif
    
    // #ifdef VUE2
    beforeCreate() {
        this.setPlatform()
    },
    // #endif
    
    mounted() {
        // 延迟初始化，确保文本渲染完成
        setTimeout(() => {
            this.initMarquee()
        }, 100)
    },

    // 监听文本变化
    watch: {
        text: {
            handler() {
                setTimeout(() => {
                    this.initMarquee()
                }, 100)
            }
        }
    },

    methods: {
        setPlatform() {
            // #ifdef MP
            this.platform = 'mp'
            // #endif
            
            // #ifdef H5
            this.platform = 'h5'
            // #endif
            
            // #ifdef APP-PLUS
            this.platform = 'app'
            // #endif
        },
        
        async initMarquee() {
            if (!this.single) return
            
            try {
                // 重置状态
                this.stopMarquee()
                this.isReady = false
                
                // 等待下一帧，确保DOM更新
                await this.$nextTick()
                
                const [textRect, containerRect] = await Promise.all([
                    this.getRect('.wht-notice-bar__text'),
                    this.getRect('.wht-notice-bar__content')
                ])
                
                if (!textRect || !containerRect) {
                    console.warn('notice-bar: Failed to get element rect')
                    return
                }
                
                this.textWidth = textRect.width
                this.containerWidth = containerRect.width
                
                console.log('文本宽度:', this.textWidth, '容器宽度:', this.containerWidth, '是否需要滚动:', this.needScroll)
                
                // 只有需要滚动时才初始化动画
                if (this.needScroll) {
                    if (this.platform === 'mp') {
                        this.initMpAnimation()
                    } else {
                        this.isReady = true
                    }
                }
            } catch (e) {
                console.error('notice-bar init error:', e)
            }
        },
        
        initMpAnimation() {
            if (!this.animation) {
                this.animation = uni.createAnimation({
                    duration: (this.textWidth + this.containerWidth) / this.speed * 1000,
                    timingFunction: 'linear',
                    delay: 0
                })
            }
            
            // 确保动画重置
            this.stopMarquee()
            this.startMarquee()
        },
        
        startMarquee() {
            if (!this.animation || !this.needScroll) return
            
            // 先重置位置
            this.animation.translateX(this.containerWidth).step({ duration: 0 })
            this.animationData = this.animation.export()
            
            // 延迟开始滚动
            setTimeout(() => {
                this.animation
                    .translateX(-this.textWidth)
                    .step()
                this.animationData = this.animation.export()
                
                // 循环播放
                setTimeout(() => {
                    this.startMarquee()
                }, (this.textWidth + this.containerWidth) / this.speed * 1000)
            }, 100)
        },
        
        stopMarquee() {
            if (this.platform === 'mp' && this.animation) {
                this.animation.translateX(0).step({ duration: 0 })
                this.animationData = this.animation.export()
            }
            this.isReady = false
        },
        
        getRect(selector) {
            return new Promise((resolve) => {
                const query = uni.createSelectorQuery()
                
                // #ifdef VUE3
                query.in(this)
                // #endif
                
                // #ifdef VUE2
                query.in(this)
                // #endif
                
                query.select(selector)
                    .boundingClientRect(rect => {
                        resolve(rect)
                    })
                    .exec()
            })
        },
        
        onClick() {
            this.$emit('click')
        },
        
        onClose() {
            this.stopMarquee()
            this.isShow = false
            this.$emit('close')
        }
    }
}
</script>

<style lang="scss" scoped>
.wht-notice-bar {
    display: flex;
    padding: 20rpx 30rpx;
    font-size: 30rpx;
    box-shadow: 0 2rpx 4rpx rgba(0, 0, 0, 0.1);
    transition: all 0.3s ease;
    
    // 主题样式
    &--primary {
        background-color: #ecf5ff;
        color: #409eff;
    }
    
    &--success {
        background-color: #f0f9eb;
        color: #67c23a;
    }
    
    &--warning {
        background-color: #fdf6ec;
        color: #e6a23c;
    }
    
    &--error {
        background-color: #fef0f0;
        color: #f56c6c;
    }
    
    &--info {
        background-color: #f4f4f5;
        color: #909399;
    }
    
    &.is-multi {
        align-items: center;
        min-height: 100rpx;
        
        .wht-notice-bar__left,
        .wht-notice-bar__right {
            padding-top: 0;
        }
    }
    
    &:not(.is-multi) {
        align-items: center;
        
      
    }
    
    &__left {
        margin-right: 24rpx;
        display: flex;
        align-items: center;
        flex-shrink: 0;
    }
    
    &__content {
        flex: 1;
        position: relative;
        overflow: hidden;
        display: flex;
        align-items: center;
    }
    
    &__text {
        display: block;
        
        &.single-line {
            white-space: nowrap;
            display: inline-block;
        }
        
        &.multi-line {
            white-space: normal;
            word-wrap: break-word;
            display: -webkit-box;
            -webkit-box-orient: vertical;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        
        &.css-animation {
            transform: translateX(var(--container-width));
            animation: notice-scroll var(--animation-duration) linear infinite;
        }
        
        // 不需要滚动时的样式
        &.no-scroll {
            transform: none !important;
            animation: none !important;
            text-overflow: ellipsis;
            overflow: hidden;
        }
    }
    
    &__right {
        margin-left: 24rpx;
        display: flex;
        align-items: center;
        flex-shrink: 0;
    }
}

@keyframes notice-scroll {
    from {
        transform: translateX(var(--container-width));
    }
    to {
        transform: translateX(calc(-1 * var(--scroll-width)));
    }
}
</style>
