<template>
	<view class="demo-select">
		<view class="demo-section">
			<view class="demo-title">基础用法</view>
			<wht-select
				v-model="value1"
				:options="options1"
				placeholder="请选择"
				@change="onChange"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">禁用状态</view>
			<wht-select
				v-model="value2"
				:options="options1"
				disabled
				placeholder="禁用状态"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义选项内容</view>
			<wht-select
				v-model="value3"
				:options="options2"
				placeholder="请选择"
			>
				<template #option="{ option }">
					<view class="custom-option">
						<text class="label">{{ option.label }}</text>
						<text class="desc">{{ option.desc }}</text>
					</view>
				</template>
			</wht-select>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">多选模式</view>
			<wht-select
				v-model="value4"
				:options="options1"
				multiple
				placeholder="请选择"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">可搜索</view>
			<wht-select
				v-model="value5"
				:options="options1"
				filterable
				placeholder="请选择"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义字段名</view>
			<wht-select
				v-model="value6"
				:options="options3"
				value-key="id"
				label-key="name"
				placeholder="请选择"
			/>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">可清空</view>
			<wht-select
				v-model="value7"
				:options="options1"
				clearable
				placeholder="请选择"
			/>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				value1: '',
				value2: '',
				value3: '',
				value4: [],
				value5: '',
				value6: '',
				value7: '',
				
				options1: [
					{ label: '选项1', value: '1' },
					{ label: '选项2', value: '2' },
					{ label: '选项3', value: '3' }
				],
				options2: [
					{ label: '选项1', value: '1', desc: '描述文字1' },
					{ label: '选项2', value: '2', desc: '描述文字2' },
					{ label: '选项3', value: '3', desc: '描述文字3' }
				],
				options3: [
					{ name: '选项1', id: '1' },
					{ name: '选项2', id: '2' },
					{ name: '选项3', id: '3' }
				]
			}
		},
		methods: {
			onChange(value) {
				uni.showToast({
					title: `当前值：${value}`,
					icon: 'none'
				})
			}
		}
	}
</script>

<style lang="scss">
.demo-select {
	padding: 20rpx;
	
	.demo-section {
		margin-bottom: 40rpx;
		
		.demo-title {
			font-size: 28rpx;
			color: #666;
			margin-bottom: 20rpx;
		}
		
		.custom-option {
			display: flex;
			flex-direction: column;
			
			.label {
				font-size: 28rpx;
				color: #323233;
			}
			
			.desc {
				font-size: 24rpx;
				color: #969799;
				margin-top: 4rpx;
			}
		}
	}
}
</style>
