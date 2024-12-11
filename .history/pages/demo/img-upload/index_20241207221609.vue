<template>
	<view class="demo-img-upload">
		<view class="demo-section">
			<view class="demo-title">基础用法</view>
			<wht-img-upload
				v-model="fileList1"
				:max-count="3"
				@after-read="afterRead"
				@delete="onDelete"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">限制上传数量</view>
			<wht-img-upload
				v-model="fileList2"
				:max-count="2"
				@after-read="afterRead"
				@delete="onDelete"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义大小</view>
			<wht-img-upload
				v-model="fileList3"
				:max-count="3"
				:image-size="100"
				@after-read="afterRead"
				@delete="onDelete"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">可预览图片</view>
			<wht-img-upload
				v-model="fileList4"
				:max-count="3"
				:preview-full-image="true"
				@after-read="afterRead"
				@delete="onDelete"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">上传前校验</view>
			<wht-img-upload
				v-model="fileList5"
				:max-count="3"
				:before-read="beforeRead"
				@after-read="afterRead"
				@delete="onDelete"
			/>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				fileList1: [],
				fileList2: [],
				fileList3: [],
				fileList4: [],
				fileList5: []
			}
		},
		methods: {
			afterRead(event) {
				const { file } = event.detail
				// 此处可以调用上传图片的接口
				console.log('开始上传图片:', file)
			},
			beforeRead(event) {
				const { file } = event.detail
				if (file.type !== 'image') {
					uni.showToast({
						title: '请选择图片文件',
						icon: 'none'
					})
					return false
				}
				return true
			},
			onDelete(event) {
				const { index } = event.detail
				console.log('删除图片，索引:', index)
			}
		}
	}
</script>

<style lang="scss">
.demo-img-upload {
	padding: 20rpx;
	
	.demo-section {
		margin-bottom: 40rpx;
		
		.demo-title {
			font-size: 28rpx;
			color: #666;
			margin-bottom: 20rpx;
		}
	}
}
</style>
