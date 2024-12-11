<template>
	<view class="demo-container">
		<view class="page-header">
			<view class="page-title">Select 选择器</view>
			<view class="page-desc">用于代替原生选择器，支持更丰富的样式定制和交互效果</view>
		</view>
		
		<view class="demo-section">

				
			<!-- 7. 可搜索 -->
			<view class="demo-card">
				<view class="card-header">
					<text class="card-title">可搜索</text>
					<text class="card-desc">支持直接输入关键词搜索选项</text>
				</view>
				<view class="card-content">
					<wht-select 
						v-model="value7" 
						:options="searchOptions"
						filterable
						:clearable="true"
						placeholder="搜索并选择城市"
						@search="handleSearch"
					/>
				</view>
			</view>
			<!-- 1. 基础用法 -->
			<view class="demo-card">
				<view class="card-header">
					<text class="card-title">基础用法</text>
					<text class="card-desc">最基础的下拉选择器用法，点击即可选择选项</text>
				</view>
				<view class="card-content">
					<wht-select 
						v-model="value1" 
						:options="options1"
						placeholder="请选择一个选项"
						@change="handleChange"
					/>
				</view>
			</view>
			
			<!-- 2. 自定义样式 -->
			<view class="demo-card">
				<view class="card-header">
					<text class="card-title">自定义样式</text>
					<text class="card-desc">支持自定义高度、颜色、圆角等样式属性</text>
				</view>
				<view class="card-content">
					<wht-select 
						v-model="value6" 
						:options="colorOptions"
						:height="48"
						:fontSize="16"
						borderColor="#8b5cf6"
						backgroundColor="#f5f3ff"
						textColor="#6d28d9"
						placeholderColor="#a78bfa"
						activeColor="#7c3aed"
						:borderRadius="8"
						:clearable="true"
						placeholder="自定义紫色主题"
					/>
				</view>
			</view>
			
			<!-- 3. 默认值 -->
			<view class="demo-card">
				<view class="card-header">
					<text class="card-title">默认值</text>
					<text class="card-desc">通过 v-model 可以指定默认选中的选项</text>
				</view>
				<view class="card-content">
					<wht-select 
						v-model="value2" 
						:options="cityOptions"
						placeholder="请选择城市"
					/>
				</view>
			</view>
			
			<!-- 4. 可清除 -->
			<view class="demo-card">
				<view class="card-header">
					<text class="card-title">可清除</text>
					<text class="card-desc">设置 clearable 属性后，选择器会显示清除按钮</text>
				</view>
				<view class="card-content">
					<wht-select 
						v-model="value3" 
						:options="options1"
						:clearable="true"
						placeholder="请选择选项"
						@clear="handleClear"
					/>
				</view>
			</view>
			
			<!-- 5. 禁用选项 -->
			<view class="demo-card">
				<view class="card-header">
					<text class="card-title">禁用选项</text>
					<text class="card-desc">可以设置 disabled 属性来禁用某些选项</text>
				</view>
				<view class="card-content">
					<wht-select 
						v-model="value4" 
						:options="disabledOptions"
						placeholder="请选择"
					/>
				</view>
			</view>
			
			<!-- 6. 禁用状态 -->
			<view class="demo-card">
				<view class="card-header">
					<text class="card-title">禁用状态</text>
					<text class="card-desc">禁用整个选择器组件</text>
				</view>
				<view class="card-content">
					<wht-select 
						v-model="value5" 
						:options="options1"
						:disabled="true"
						placeholder="禁用状态"
					/>
				</view>
			</view>
		
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			value1: '',
			value2: 'beijing',
			value3: '',
			value4: '',
			value5: '',
			value6: '',
			value7: '',
			
			// 基础选项
			options1: [
				{ label: '选项一', value: '1' },
				{ label: '选项二', value: '2' },
				{ label: '选项三', value: '3' }
			],
			// 城市选项
			cityOptions: [
				{ label: '北京', value: 'beijing' },
				{ label: '上海', value: 'shanghai' },
				{ label: '广州', value: 'guangzhou' },
				{ label: '深圳', value: 'shenzhen' }
			],
			// 禁用选项示例
			disabledOptions: [
				{ label: '可选项 A', value: 'a' },
				{ label: '禁用选项', value: 'b', disabled: true },
				{ label: '可选项 B', value: 'c' },
				{ label: '禁用选项', value: 'd', disabled: true }
			],
			// 颜色主题选项
			colorOptions: [
				{ label: '薰衣草紫', value: 'lavender' },
				{ label: '靛青蓝', value: 'indigo' },
				{ label: '玫瑰粉', value: 'rose' },
				{ label: '翡翠绿', value: 'emerald' }
			],
			// 搜索示例选项
			searchOptions: [
				{ label: '北京市', value: 'beijing' },
				{ label: '上海市', value: 'shanghai' },
				{ label: '广州市', value: 'guangzhou' },
				{ label: '深圳市', value: 'shenzhen' },
				{ label: '杭州市', value: 'hangzhou' },
				{ label: '南京市', value: 'nanjing' },
				{ label: '成都市', value: 'chengdu' },
				{ label: '武汉市', value: 'wuhan' },
				{ label: '西安市', value: 'xian' },
				{ label: '重庆市', value: 'chongqing' }
			]
		}
	},
	methods: {
		handleChange(item) {
			console.log('选中项：', item)
		},
		handleClear() {
			console.log('已清除选中项')
		},
		handleSearch(query) {
			console.log('搜索关键词：', query)
		}
	}
}
</script>

<style lang="scss" scoped>
.demo-container {
	min-height: 100vh;
	padding: 20px;
	background-color: #f5f7fa;
	
	.page-header {
		margin-bottom: 24px;
		padding-left: 12px;
		position: relative;
		
		&::before {
			content: '';
			position: absolute;
			left: 0;
			top: 50%;
			transform: translateY(-50%);
			width: 4px;
			height: 18px;
			background: linear-gradient(180deg, #409eff, #40b9ff);
			border-radius: 2px;
		}
	}
}

.demo-section {
	display: flex;
	flex-wrap: wrap;
	justify-content: space-between;
}

.demo-card {
	width: 100%;
	max-width: 800px;
	margin: 0 auto 20px;
	border-radius: 12px;
	background: #ffffff;
	box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
	
	.card-header {
		padding: 16px 20px;
		border-bottom: 1px solid #f0f0f0;
		background: linear-gradient(to right, #fafafa, #ffffff);
		
		.card-title {
			display: block;
			font-size: 16px;
			font-weight: 600;
			color: #1a1a1a;
			margin-bottom: 8px;
		}
		
		.card-desc {
			font-size: 14px;
			color: #999;
			line-height: 1.5;
		}
	}
	
	.card-content {
		padding: 20px;
	}
}

// 暗黑模式适配
@media (prefers-color-scheme: dark) {
	.demo-container {
		background-color: #1a1a1a;
		
		.page-title {
			color: #ffffff;
		}
	}
	
	.demo-card {
		background: #2c2c2e;
		box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
		
		.card-header {
			border-bottom-color: #3a3a3c;
			background: linear-gradient(to right, #2c2c2e, #323234);
			
			.card-title {
				color: #ffffff;
			}
			
			.card-desc {
				color: #8e8e93;
			}
		}
	}
}
</style>
