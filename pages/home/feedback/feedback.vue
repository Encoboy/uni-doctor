<template>
	<view class="hospital-box" :style="{ height: windowHeight + 'px' }">
		<view class="header-img-box">
			<image src="../../../static/img/title-img.png" mode="aspectFit"></image>
		</view>
		<view class="content-box">
			<view class="header-title">
				医生反馈
			</view>
			<view class="text-area">
				<u-input style="background-color: white;" v-model="value" :type="type" :border="border" :height="height" :auto-height="autoHeight" />
			</view>
			<view class="btn-box">
				<view class="btn">
					保存
				</view>
				<view class="btn cancel">
					取消
				</view>
			</view>
		</view>

	</view>
</template>

<script>
	import LineChart from '@/components/stan-ucharts/LineChart.vue';
	export default {
		components: {
			LineChart,
		},
		data() {
			return {
				title: 'Hello',
				windowHeight:0,
				value: '',
				type: 'textarea',
				border: true,
				height: 500,
				autoHeight: true,
			}
		},
		onLoad() {
			const res = uni.getSystemInfoSync();
			this.windowHeight = res.windowHeight;
		},
		methods: {
		}
	}
</script>

<style lang="scss">
	.hospital-box{
		.content-box{
			flex: 8.5;
			flex-basis: 0;
			border: 1px solid black;
			margin-bottom: 30rpx;
			padding-top: 30rpx;
			background-color: #bdf2e5;
			.header-title {
				flex: 1;
				flex-basis: 0;
				font-size: 80rpx;
				text-align: center;
				color: #666666;
			}
			.text-area {
				padding: 20rpx;
			}
			.btn-box {
				display: flex;
				flex-direction: row;
				justify-content: space-around;
				margin-top: 50rpx;
				.btn{
					width: 250rpx;
					height: 80rpx;
					color: white;
					border-radius: 10px;
					background-color: #169bd5;
					text-align: center;
					line-height: 80rpx;
				}
				.cancel {
					background-color: #cccccc;
				}
			}
		}


	}
</style>
