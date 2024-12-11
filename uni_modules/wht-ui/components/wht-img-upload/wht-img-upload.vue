<template>
  <view class="wht-upload-container">
    <view class="wht-upload-list" :class="{ 'single-mode': mode === 'single' }" :style="listStyle">
      <view v-for="(item, index) in imageList" :key="index" class="wht-upload-item"
        :class="{ 'single-item': mode === 'single' }" :style="itemStyle">
        <image :src="item" :mode="mode === 'single' ? 'aspectFit' : 'aspectFill'" @tap="previewImage(index)"
          class="upload-image" />
        <view class="delete-btn" @tap.stop="deleteImage(index)">
          <text class="iconfont icon-close">×</text>
        </view>
        ---- {{ uploadStatus }}
        <view v-if="uploadStatus[index]?.isLoading" class="loading-overlay">
          <view class="progress-container">
            <view class="progress-bar">
              <view class="progress-inner" :style="{ width: `${uploadStatus[index]?.progress || 0}%` }"></view>
            </view>
            <text class="progress-text">{{ uploadStatus[index]?.progress || 0 }}%</text>
          </view>
        </view>
      </view>
      <view v-if="imageList.length < max" class="wht-upload-button" :class="{
        'single-button': mode === 'single',
        'no-text': !showButtonText
      }" @tap="chooseImage" :style="itemStyle">
        <text class="icon-add" :class="{ 'no-margin': !showButtonText }">+</text>
        <text v-if="showButtonText" class="upload-text">{{ buttonText }}</text>
      </view>
    </view>
  </view>
</template>

<script>
// 定义一个工具函数来处理不同Vue版本的emit
const emitEvent = (ctx, eventName, ...args) => {
  if (ctx.$emit) {
    // Vue 2
    ctx.$emit(eventName, ...args)
  } else {
    // Vue 3
    ctx.emit(eventName, ...args)
  }
}

export default {
  name: 'wht-img-upload',
  props: {
    imageFormat: {
      type: Array,
      default: () => ['jpg', 'jpeg', 'png'] // 默认支持的图片格式
    },
    max: {
      type: Number,
      default: 9
    },
    modelValue: {
      type: Array,
      default: () => []
    },
    buttonText: {
      type: String,
      default: '上传图片'
    },
    showButtonText: {
      type: Boolean,
      default: true
    },
    mode: {
      type: String,
      default: 'multi',
      validator: value => ['multi', 'single'].includes(value)
    },
    columns: {
      type: Number,
      default: 3
    },
    itemWidth: {
      type: Number,
      default: 0
    },
    itemHeight: {
      type: Number,
      default: 216
    },
    gap: {
      type: Number,
      default: 24
    },
    name: {
      type: String,
      default: 'file'
    },
    // 上传相关配置
    uploadConfig: {
      type: Object,
      default: () => ({
        // 上传地址
        url: '',
        // 文件字段名
        name: 'file',
        // 请求头
        header: {},
        // 附带的表单数据
        formData: {},
        // 是否开启实际上传
        enabled: true
      })
    },
  },

  computed: {
    containerWidth() {
      if (this.mode === 'single') {
        return this.itemWidth
      }
      return this.itemWidth
    },

    listStyle() {
      if (this.mode === 'single') {
        return {
          gap: `${this.gap}rpx`,
        }
      }
      return {
        gap: `${this.gap}rpx`,
      }
    },

    itemStyle() {
      if (this.mode === 'single') {
        return {
          width: '100%',
          height: `${this.itemHeight}rpx`
        }
      }
      return {
        width: `${this.calculatedItemWidth}rpx`,
        height: `${this.calculatedItemHeight}rpx`
      }
    },
    // 获取实际的值（兼容 Vue2/3）
    actualValue() {
      return this.modelValue
    }
  },

  data() {
    return {
      imageList: [],
      uploadStatus: [], // 每个图片的上传状态 { index: { isLoading: boolean, progress: number } }
      calculatedItemWidth: 0,
      calculatedItemHeight: 0
    }
  },

  watch: {
    actualValue: {
      handler(val) {
        console.log('actualValue changed：', val);
        this.imageList = val
      },
      immediate: true
    }
  },

  methods: {
    // 选择图片
    async chooseImage() {
      try {
        const count = this.mode === 'single' ? 1 : this.max - this.imageList.length;
        const res = await uni.chooseImage({
          count: count,
          sizeType: ['original', 'compressed'],
          sourceType: ['album', 'camera']
        });

        // const validImages = res.tempFilePaths.filter(filePath => {
        //   const extension = filePath.split('.').pop().toLowerCase();
        //   return this.imageFormat.includes(extension);
        // });
        const validImages = res.tempFilePaths;

        // if (validImages.length === 0) {
        //   uni.showToast({
        //     title: '没有符合格式的图片',
        //     icon: 'none'
        //   });
        //   return;
        // }

        if (this.mode === 'single') {
          this.imageList = [validImages[0]];
          emitEvent(this, 'update:modelValue', this.imageList);

          // 设置上传状态
          this.$set(this.uploadStatus, 0, {
            isLoading: true,
            progress: 0
          });

          let res = null;
          if (this.uploadConfig.enabled && this.uploadConfig.url) {
            res = await this.uploadFile(validImages[0], 0);
          } else {
            res = await this.simulateUpload(validImages[0], 0);
          }
          this.imageList = [res.url];
          console.log('this.imageList：', res);
        } else {
          const startIndex = this.imageList.length;
          const newImages = [...this.imageList, ...validImages];
          this.imageList = newImages;
          emitEvent(this, 'update:modelValue', newImages);

          for (let i = 0; i < validImages.length; i++) {
            const currentIndex = startIndex + i;
            // 设置每张图片的上传状态
            this.$set(this.uploadStatus, currentIndex, {
              isLoading: true,
              progress: 0
            });

            if (this.uploadConfig.enabled && this.uploadConfig.url) {
              this.uploadFile(validImages[i], currentIndex)
                .then(res => {
                  this.imageList[currentIndex] = res.url;
                });
            } else {
              this.simulateUpload(validImages[i], currentIndex)
                .then(res => {
                  this.imageList[currentIndex] = res.url;
                });
            }
          }
        }
        emitEvent(this, 'update:modelValue', this.imageList);
        emitEvent(this, 'choose', validImages);
      } catch (error) {
        console.error('选择图片失败：', error);
        emitEvent(this, 'error', error);
      }
    },

    // 实际的文件上传方法
    uploadFile(filePath, index) {
      return new Promise((resolve, reject) => {
        const uploadTask = uni.uploadFile({
          url: this.uploadConfig.url,
          filePath: filePath,
          name: this.uploadConfig.name,
          header: this.uploadConfig.header,
          formData: this.uploadConfig.formData,
          success: (uploadRes) => {
            try {
              // 更新上传状态为完成
              this.$set(this.uploadStatus, index, {
                isLoading: false,
                progress: 100
              });
              console.log('uploadRes：', uploadRes);
              resolve(JSON.parse(uploadRes.data));
            } catch (e) {
              reject(e);
            }
          },
          fail: (err) => {
            // 更新上传状态为失败
            this.$set(this.uploadStatus, index, {
              isLoading: false,
              progress: 0
            });
            emitEvent(this, 'error', { error: err, index });
            reject(err);
          }
        });

        uploadTask.onProgressUpdate((res) => {
          console.log('onProgressUpdate ', res)
          // 更新对应图片的上传进度
          this.$set(this.uploadStatus, index, {
            isLoading: true,
            progress: res.progress
          });
          emitEvent(this, 'progress', {
            index,
            progress: res.progress
          });
        });
      });
    },

    // 模拟上传进度
    simulateUpload(filePath, index) {
      return new Promise((resolve) => {
        let progress = 0;
        const timer = setInterval(() => {
          progress += 10;
          this.$set(this.uploadStatus, index, {
            isLoading: true,
            progress
          });

          if (progress >= 100) {
            clearInterval(timer);
            setTimeout(() => {
              this.$set(this.uploadStatus, index, {
                isLoading: false,
                progress: 100
              });
              resolve({ url: filePath });
            }, 200);
          }
        }, 200);
      });
    },

    // 删除图片时清除对应的上传状态
    deleteImage(index) {
      this.imageList.splice(index, 1);
      this.$delete(this.uploadStatus, index);
      emitEvent(this, 'update:modelValue', this.imageList);
      emitEvent(this, 'delete', index);
    },

    // 预览图片
    previewImage(index) {
      uni.previewImage({
        urls: this.imageList,
        current: index
      });
    },

    // 计算项目宽度
    calculateItemWidth() {
      const query = uni.createSelectorQuery().in(this);
      query.select('.wht-upload-list').boundingClientRect(data => {
        if (data) {
          // 将px转换为rpx
          const screenWidth = uni.getSystemInfoSync().windowWidth;
          const containerWidthRpx = (data.width * 750) / screenWidth;

          // 计算单个项目宽度：(容器宽度 - 总间距) / 列数
          const totalGap = this.gap * (this.columns - 1);
          this.calculatedItemWidth = (containerWidthRpx - totalGap) / this.columns;

          // 设高度等于宽度，保持正方形
          this.calculatedItemHeight = this.calculatedItemWidth;
        }
      }).exec();
    }
  },

  mounted() {
    this.calculateItemWidth();
    // 使用 uni.onWindowResize 监听窗口大小变化
    uni.onWindowResize(this.calculateItemWidth);
  },

  beforeDestroy() {
    // 使用 uni.offWindowResize 移除监听
    uni.offWindowResize(this.calculateItemWidth);
  }
}
</script>

<style lang="scss" scoped>
.wht-upload-container {
  width: 100%;

  .wht-upload-list {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;

    &.single-mode {
      flex-direction: column;
      width: 100%;
    }
  }

  .wht-upload-item {
    position: relative;
    border-radius: 16rpx;
    overflow: hidden;
    box-shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.08);
    flex-shrink: 0;

    &.single-item {
      width: 100%;
      margin-bottom: 20rpx;

      .upload-image {
        width: 100%;
        height: 100%;
        object-fit: contain;
      }
    }

    .upload-image {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .delete-btn {
      position: absolute;
      top: 12rpx;
      right: 12rpx;
      width: 44rpx;
      height: 44rpx;
      background: rgba(0, 0, 0, 0.6);
      backdrop-filter: blur(4px);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #fff;
      font-size: 24rpx;
      z-index: 1;
    }
  }

  .wht-upload-button {
    background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
    border-radius: 16rpx;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: #666;
    position: relative;
    overflow: hidden;
    box-shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.06);
    flex-shrink: 0;

    &.single-button {
      width: 100%;
      background: linear-gradient(135deg, #f5f7fa 0%, #e4e7eb 100%);

      .icon-add {
        font-size: 72rpx;
      }

      .upload-text {
        font-size: 28rpx;
      }
    }

    .icon-add {
      font-size: 64rpx;
      margin-bottom: 12rpx;

      &.no-margin {
        margin-bottom: 0;
      }
    }

    .upload-text {
      font-size: 26rpx;
      font-weight: 500;
    }
  }

  .loading-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(255, 255, 255, 0.8);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    z-index: 2;

    .progress-bar {
      width: 80%;
      height: 8rpx;
      background: #f0f0f0;
      border-radius: 4rpx;
      overflow: hidden;
      margin-bottom: 10rpx;

      .progress-inner {
        height: 100%;
        background: linear-gradient(90deg, #007AFF, #00b4ff);
        transition: width 0.2s ease-out;
      }
    }

    .progress-text {
      font-size: 24rpx;
      color: #333;
    }
  }
}
</style>