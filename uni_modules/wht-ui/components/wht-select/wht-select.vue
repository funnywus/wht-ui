<template>
	<view class="wht-select-wrapper" :class="{ 'is-disabled': disabled }">
		<view 
			class="wht-select-inner"
			:class="{ 
				'is-active': isOpen,
				'is-placeholder': !currentValue
			}"
			:style="{
				height: height + 'px',
				backgroundColor: backgroundColor,
				borderColor: borderColor,
				borderRadius: borderRadius + 'px'
			}"
			@click="togglePicker"
		>
			<view class="wht-select-value">
				<input
					v-if="filterable"
					class="wht-select-input"
					v-model="searchQuery"
					:placeholder="currentValue ? currentLabel : placeholder"
					:style="{
						fontSize: fontSize + 'px',
						color: currentValue ? textColor : placeholderColor
					}"
					@click.stop
					@input="onSearch"
					@focus="handleFocus"
				/>
				<text
					v-else
					:style="{
						fontSize: fontSize + 'px',
						color: currentValue ? textColor : placeholderColor
					}"
				>{{ currentLabel || placeholder }}</text>
			</view>
			<view class="wht-select-suffix">
				<view 
					v-if="clearable && currentValue && !disabled" 
					class="wht-select-clear"
					@click.stop="clearValue"
				>×</view>
				<view 
					v-else 
					class="wht-select-arrow"
					:style="{ borderTopColor: placeholderColor }"
				></view>
			</view>
		</view>
		<view v-if="isOpen" class="select-dropdown">
			<view class="select-dropdown-mask" @click.stop="togglePicker"></view>
			<view 
				class="select-dropdown-content"
				:style="{
					backgroundColor: backgroundColor,
					borderRadius: borderRadius + 'px'
				}"
			>
				<template v-if="filteredOptions.length > 0">
					<view 
						v-for="(item, index) in filteredOptions" 
						:key="item.value" 
						:class="{ 
							'disabled': item.disabled,
							'active': currentValue === item.value
						}"
						:style="{
							fontSize: fontSize + 'px',
							color: item.disabled ? placeholderColor : textColor,
							backgroundColor: currentValue === item.value ? activeColor + '20' : backgroundColor
						}"
						@click.stop="selectOption(item, index)"
					>
						{{ item.label }}
					</view>
				</template>
				<view 
					v-else 
					class="select-dropdown-empty"
					:style="{
						fontSize: fontSize + 'px',
						color: placeholderColor
					}"
				>
					暂无数据
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	name: 'wht-select',
	props: {
		options: {
			type: Array,
			default: () => []
		},
		value: {
			type: [String, Number],
			default: ''
		},
		placeholder: {
			type: String,
			default: '请选择'
		},
		disabled: {
			type: Boolean,
			default: false
		},
		clearable: {
			type: Boolean,
			default: false
		},
		// 样式相关的props
		height: {
			type: Number,
			default: 40
		},
		fontSize: {
			type: Number,
			default: 14
		},
		borderColor: {
			type: String,
			default: '#dcdfe6'
		},
		borderRadius: {
			type: Number,
			default: 4
		},
		backgroundColor: {
			type: String,
			default: '#ffffff'
		},
		textColor: {
			type: String,
			default: '#606266'
		},
		placeholderColor: {
			type: String,
			default: '#c0c4cc'
		},
		activeColor: {
			type: String,
			default: '#409eff'
		},
		filterable: {
			type: Boolean,
			default: false
		},
		searchPlaceholder: {
			type: String,
			default: '请输入搜索内容'
		}
	},
	data() {
		return {
			currentValue: '',
			isOpen: false,
			searchQuery: ''
		}
	},
	computed: {
		currentLabel() {
			const option = this.options.find(item => item.value === this.currentValue)
			return option ? option.label : ''
		},
		filteredOptions() {
			if (!this.filterable || !this.searchQuery) {
				return this.options
			}
			return this.options.filter(item => 
				item.label.toLowerCase().includes(this.searchQuery.toLowerCase())
			)
		}
	},
	watch: {
		value: {
			handler(newVal) {
				this.currentValue = newVal
			},
			immediate: true
		}
	},
	methods: {
		togglePicker() {
			if (this.disabled) return
			this.isOpen = !this.isOpen
			if (!this.isOpen) {
				this.searchQuery = ''
			}
		},
		selectOption(item, index) {
			if (item.disabled) return
			this.currentValue = item.value
			this.searchQuery = ''
			this.$emit('input', item.value)
			this.$emit('change', item)
			this.isOpen = false
		},
		clearValue(e) {
			this.currentValue = ''
			this.searchQuery = ''
			this.$emit('input', '')
			this.$emit('change', null)
			this.$emit('clear')
		},
		onSearch() {
			this.$emit('search', this.searchQuery)
		},
		handleFocus() {
			if (!this.disabled) {
				this.isOpen = true
			}
		}
	}
}
</script>

<style lang="scss" scoped>
.wht-select-wrapper {
	width: 100%;
	position: relative;
	
	.wht-select-inner {
		position: relative;
		width: 100%;
		border-width: 1px;
		border-style: solid;
		transition: all 0.2s;
		cursor: pointer;
		
		&.is-active {
			.wht-select-arrow {
				transform: rotate(180deg);
			}
		}
	}
	
	.wht-select-value {
		position: absolute;
		left: 12px;
		right: 30px;
		top: 50%;
		transform: translateY(-50%);
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
		height: 100%;
		display: flex;
		align-items: center;
	}
	
	.wht-select-suffix {
		position: absolute;
		right: 8px;
		top: 50%;
		transform: translateY(-50%);
		display: flex;
		align-items: center;
	}
	
	.wht-select-clear {
		width: 16px;
		height: 16px;
		line-height: 16px;
		text-align: center;
		border-radius: 50%;
		background-color: #c0c4cc;
		color: #fff;
		font-size: 12px;
		cursor: pointer;
		transition: all 0.2s;
		
		&:hover {
			background-color: #909399;
		}
	}
	
	.wht-select-arrow {
		width: 0;
		height: 0;
		border-left: 5px solid transparent;
		border-right: 5px solid transparent;
		border-top: 5px solid;
		transition: transform 0.2s;
	}
	
	.select-dropdown {
		position: absolute;
		top: 100%;
		left: 0;
		width: 100%;
		margin-top: 4px;
		z-index: 999;
	}
	
	.select-dropdown-mask {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		z-index: 998;
	}
	
	.select-dropdown-content {
		position: relative;
		max-height: 240px;
		border: 1px solid #e4e7ed;
		box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
		z-index: 999;
		overflow-y: auto;
		
		&::-webkit-scrollbar {
			width: 6px;
		}
		
		&::-webkit-scrollbar-thumb {
			background-color: #e4e7ed;
			border-radius: 3px;
		}
		
		> view {
			padding: 0 12px;
			height: 36px;
			line-height: 36px;
			cursor: pointer;
			
			&.disabled {
				cursor: not-allowed;
			}
		}
		
		.select-dropdown-search {
			padding: 8px;
			border-bottom: 1px solid #e4e7ed;
			
			input {
				width: 100%;
				height: 32px;
				padding: 0 8px;
				border: 1px solid #dcdfe6;
				border-radius: 4px;
				font-size: 14px;
				
				&:focus {
					border-color: #409eff;
					outline: none;
				}
			}
		}
		
		.select-dropdown-empty {
			padding: 12px;
			text-align: center;
		}
	}
	
	.wht-select-input {
		width: 100%;
		height: 100%;
		background: transparent;
		border: none;
		outline: none;
		padding: 0;
		margin: 0;
		line-height: normal;
		
		&::placeholder {
			color: inherit;
			line-height: normal;
		}
	}
}

// 暗黑模式适配
@media (prefers-color-scheme: dark) {
	.wht-select-wrapper {
		.select-dropdown-content {
			box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.3);
			
			&::-webkit-scrollbar-thumb {
				background-color: #48484a;
			}
			
			.select-dropdown-search {
				border-bottom-color: #48484a;
				
				input {
					border-color: #48484a;
					background-color: #1c1c1e;
					color: #fff;
					
					&:focus {
						border-color: #409eff;
					}
				}
			}
		}
	}
}
</style>