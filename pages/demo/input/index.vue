<template>
	<view class="content">
		<!-- 基础输入框 -->
		<text class="section-title">基础输入框</text>
		<wht-input 
			v-model="input1" 
			placeholder="默认输入框"
		></wht-input>

		
		<!-- 事件演示 -->
		<text class="section-title">事件演示</text>
		
		<!-- 输入事件 -->
		<wht-input 
			v-model="inputValue"
			placeholder="输入事件演示"
			clearable
			@input="onInput"
			@focus="onFocus"
			@blur="onBlur"
			@clear="onClear"
			@confirm="onConfirm"
		></wht-input>
		
		<!-- 带图标的输入框 -->
		<text class="section-title">带图标的输入框</text>
		<wht-input 
			v-model="input2" 
			 prefix-icon="search"
			placeholder="搜索框"
		></wht-input>
		
		<!-- 主题色输入框 -->
		<view class="theme-section">
			<text class="section-title">主题色输入框</text>
			
			<!-- 蓝色主题 -->
			<wht-input 
				v-model="input3" 
				border-color="#409eff"
				text-color="#409eff"
				icon-color="#409eff"
				placeholder="蓝色主题"
			></wht-input>
			
			<!-- 绿色主题 -->
			<wht-input 
				v-model="input4"
				border-color="#67c23a"
				background-color="#f0f9eb"
				text-color="#67c23a"
				placeholder="绿色主题"
				placeholder-color="#85ce61"
			></wht-input>
			
			<!-- 警告色主题 -->
			<wht-input 
				v-model="input5"
				prefix-icon="search"
				border-color="#e6a23c"
				text-color="#e6a23c"
				icon-color="#e6a23c"
				placeholder="警告色主题"
			></wht-input>
			
			<!-- 红色主题 -->
			<wht-input 
				v-model="input6"
				border-color="#f56c6c"
				background-color="#fef0f0"
				text-color="#f56c6c"
				icon-color="#f56c6c"
				placeholder="红色主题"
				prefix-icon="search"
			></wht-input>
		</view>
		
		<!-- 圆角演示 -->
		<view class="radius-section">
			<text class="section-title">圆角演示</text>
			
			<!-- 无圆角 -->
			<wht-input 
				v-model="input7"
				:radius="0"
				placeholder="无圆角"
			></wht-input>
			
			<!-- 大圆角 -->
			<wht-input 
				v-model="input8"
				:radius="20"
				placeholder="大圆角"
			></wht-input>
		</view>
		
		<!-- 功能型输入框 -->
		<view class="feature-section">
			<text class="section-title">功能型输入框</text>
			
			<!-- 可清除输入框 -->
			<wht-input 
				v-model="input9"
				clearable
				placeholder="可清除输入框"
			></wht-input>
			
			<!-- 密码输入框 -->
			<wht-input 
				v-model="input10"
				type="password"
				placeholder="密码输入框"
			></wht-input>
			
			<!-- 带前后缀的输入框 -->
			<wht-input 
				v-model="input11"
				placeholder="带前后缀的输入框"
			>
				<template #prefix>￥</template>
				<template #suffix>.00</template>
			</wht-input>
			
			<!-- 禁用状态 -->
			<wht-input 
				v-model="input12"
				disabled
				placeholder="禁用状态"
			></wht-input>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				input1: '',
				input2: '',
				input3: '',
				input4: '',
				input5: '',
				input6: '',
				input7: '',
				input8: '',
				input9: '',
				input10: '',
				input11: '',
				input12: '',
				inputValue: ''
			}
		},
		methods: {
			// 输入事件
			onInput(e) {
				console.log('输入值：', e.detail.value)
			},
			
			// 获得焦点
			onFocus() {
				console.log('输入框获得焦点')
			},
			
			// 失去焦点
			onBlur() {
				console.log('输入框失去焦点')
			},
			
			// 清空事件
			onClear() {
				console.log('输入框已清空')
			},
			
			// 确认事件
			onConfirm() {
				console.log('输入框已确认')
			}
		}
	}
</script>

<style>
	.content {
		padding: 15px;
	}

	.wht-input-wrapper {
		margin-bottom: 15px;
	}

	.section-title {
		display: block;
		margin: 20px 0 10px;
		font-size: 16px;
		color: #606266;
	}

	.theme-section,
	.radius-section,
	.feature-section {
		margin-top: 20px;
	}
</style>
