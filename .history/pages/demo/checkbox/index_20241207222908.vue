<template>
	<view class="content">
		<!-- 基础用法 -->
		<view class="demo-block">
			<text class="demo-title">基础用法</text>
			<wht-checkbox v-model="checked1">选项1</wht-checkbox>
		</view>

		<!-- 自定义颜色 -->
		<view class="demo-block">
			<text class="demo-title">自定义颜色</text>
			<view class="color-group">
				<wht-checkbox v-model="checked2" activeColor="#07c160">
					绿色主题
				</wht-checkbox>
				<wht-checkbox v-model="checked3" activeColor="#ff4d4f">
					红色主题
				</wht-checkbox>
				<wht-checkbox v-model="checked4" activeColor="#f0a020">
					橙色主题
				</wht-checkbox>
			</view>
		</view>

		<!-- 形状展示 -->
		<view class="demo-block">
			<text class="demo-title">形状展示</text>
			<view class="shape-group">
				<wht-checkbox v-model="checked5" shape="square">
					方形选择框
				</wht-checkbox>
				<wht-checkbox v-model="checked6" shape="round">
					圆形选择框
				</wht-checkbox>
			</view>
		</view>

		<!-- 禁用状态 -->
		<view class="demo-block">
			<text class="demo-title">禁用状态</text>
			<view class="disabled-group">
				<wht-checkbox v-model="checked7" disabled>
					禁用未选中
				</wht-checkbox>
				<wht-checkbox v-model="checked8" disabled>
					禁用已选中
				</wht-checkbox>
			</view>
		</view>

		<!-- 列表模式-方形 -->
		<view class="demo-block">
			<text class="demo-title">列表模式-方形</text>
			<wht-checkbox v-model="checkedList1" :options="listOptions" shape="square" isList @change="onListChange" />
		</view>

		<!-- 列表模式-圆形 -->
		<view class="demo-block">
			<text class="demo-title">列表模式-圆形</text>
			<wht-checkbox v-model="checkedList2" :options="listOptions" shape="round" isList @change="onListChange" />
		</view>

		<!-- 行内布局 -->
		<view class="demo-block">
			<text class="demo-title">行内布局</text>
			<wht-checkbox v-model="checkedList3" :options="inlineOptions" shape="square" inline isList
				@change="onListChange" />
		</view>

		<!-- 行内布局-自定义颜色 -->
		<view class="demo-block">
			<text class="demo-title">行内布局-自定义颜色</text>
			<wht-checkbox v-model="checkedList4" :options="inlineOptions" shape="round" activeColor="#07c160" inline
				isList @change="onListChange" />
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			// 基础用法
			checked1: false,
			// 自定义颜色
			checked2: true,
			checked3: true,
			checked4: true,
			// 形状展示
			checked5: true,
			checked6: true,
			// 禁用状态
			checked7: false,
			checked8: true,
			// 列表模式
			checkedList1: ['1'],
			checkedList2: ['1'],
			checkedList3: ['1'],
			checkedList4: ['1'],
			// 列表数据
			listOptions: [
				{ label: '选项一', value: '1' },
				{ label: '选项二', value: '2' },
				{ label: '选项三', value: '3' },
				{ label: '禁用选项', value: '4', disabled: true }
			],
			// 行内布局数据
			inlineOptions: [
				{ label: '选项A', value: '1' },
				{ label: '选项B', value: '2' },
				{ label: '选项C', value: '3' },
				{ label: '选项D', value: '4' },
				{ label: '选项E', value: '5' },
				{ label: '禁用项', value: '6', disabled: true }
			]
		}
	},

	methods: {
		onListChange(value) {
			console.log('当前选中:', value)
		}
	}
}
</script>

<style scoped>
.content {
	padding: 30rpx;
	background-color: #f7f8fa;
	min-height: 100vh;
}

.demo-block {
	margin-bottom: 30rpx;
	/* 减小块之间的间距 */
	padding: 24rpx;
	/* 减小内边距 */
	background-color: #fff;
	border-radius: 12rpx;
}

.demo-title {
	margin-bottom: 16rpx;
	/* 减小标题底部间距 */
	font-size: 32rpx;
	font-weight: 600;
	color: #323233;
	display: block;
}

.color-group,
.shape-group,
.disabled-group {
	display: flex;
	flex-direction: column;
	gap: 16rpx;
	/* 减小选项之间的间距 */
}

/* 暗黑模式适配 */
@media (prefers-color-scheme: dark) {
	.content {
		background-color: #121212;
	}

	.demo-block {
		background-color: #1a1a1a;
	}

	.demo-title {
		color: #fff;
	}
}
</style>