<template>
	<view class="demo-lottery">
		<view class="demo-section">
			<view class="demo-title">基础用法</view>
			<wht-lottery
				:prizes="prizes"
				:active-index="activeIndex"
				:speed="speed"
				:duration="duration"
				@end="onLotteryEnd"
			>
				<template #item="{ prize }">
					<view class="prize-item">
						<image :src="prize.image" mode="aspectFit" />
						<text>{{ prize.name }}</text>
					</view>
				</template>
			</wht-lottery>
			<view class="lottery-action">
				<wht-button type="primary" :disabled="isPlaying" @click="startLottery">
					{{ isPlaying ? '抽奖中...' : '开始抽奖' }}
				</wht-button>
			</view>
		</view>
		
		<view class="demo-section">
			<view class="demo-title">自定义样式</view>
			<wht-lottery
				:prizes="prizes"
				:active-index="activeIndex2"
				:speed="speed"
				:duration="duration"
				class="custom-lottery"
				@end="onLotteryEnd"
			>
				<template #item="{ prize }">
					<view class="prize-item custom">
						<image :src="prize.image" mode="aspectFit" />
						<text>{{ prize.name }}</text>
					</view>
				</template>
			</wht-lottery>
			<view class="lottery-action">
				<wht-button type="primary" :disabled="isPlaying2" @click="startLottery2">
					{{ isPlaying2 ? '抽奖中...' : '开始抽奖' }}
				</wht-button>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				prizes: [
					{ id: 1, name: '一等奖', image: '/static/demo/prize1.png' },
					{ id: 2, name: '二等奖', image: '/static/demo/prize2.png' },
					{ id: 3, name: '三等奖', image: '/static/demo/prize3.png' },
					{ id: 4, name: '四等奖', image: '/static/demo/prize4.png' },
					{ id: 5, name: '五等奖', image: '/static/demo/prize5.png' },
					{ id: 6, name: '六等奖', image: '/static/demo/prize6.png' },
					{ id: 7, name: '七等奖', image: '/static/demo/prize7.png' },
					{ id: 8, name: '八等奖', image: '/static/demo/prize8.png' }
				],
				activeIndex: -1,
				activeIndex2: -1,
				speed: 100,
				duration: 4000,
				isPlaying: false,
				isPlaying2: false
			}
		},
		methods: {
			startLottery() {
				if (this.isPlaying) return
				this.isPlaying = true
				// 模拟请求后端获取中奖结果
				setTimeout(() => {
					const randomIndex = Math.floor(Math.random() * this.prizes.length)
					this.activeIndex = randomIndex
				}, 500)
			},
			startLottery2() {
				if (this.isPlaying2) return
				this.isPlaying2 = true
				setTimeout(() => {
					const randomIndex = Math.floor(Math.random() * this.prizes.length)
					this.activeIndex2 = randomIndex
				}, 500)
			},
			onLotteryEnd(index) {
				this.isPlaying = false
				this.isPlaying2 = false
				uni.showToast({
					title: `恭喜获得${this.prizes[index].name}`,
					icon: 'none'
				})
			}
		}
	}
</script>

<style lang="scss">
.demo-lottery {
	padding: 20rpx;
	
	.demo-section {
		margin-bottom: 40rpx;
		
		.demo-title {
			font-size: 28rpx;
			color: #666;
			margin-bottom: 20rpx;
		}
		
		.lottery-action {
			margin-top: 30rpx;
			padding: 0 40rpx;
		}
		
		.prize-item {
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
			height: 100%;
			
			image {
				width: 60rpx;
				height: 60rpx;
				margin-bottom: 10rpx;
			}
			
			text {
				font-size: 24rpx;
				color: #333;
			}
			
			&.custom {
				background-color: #fff7e6;
				border-radius: 12rpx;
				
				image {
					width: 80rpx;
					height: 80rpx;
				}
				
				text {
					color: #ff6b00;
				}
			}
		}
		
		.custom-lottery {
			--wht-lottery-item-size: 200rpx;
			--wht-lottery-gap: 20rpx;
			--wht-lottery-border-radius: 20rpx;
			--wht-lottery-border-color: #ff6b00;
			--wht-lottery-active-shadow: 0 0 20rpx rgba(255, 107, 0, 0.3);
		}
	}
}
</style>
