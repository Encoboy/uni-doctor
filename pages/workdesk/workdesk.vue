<template>
	<view class="hospital-box" :style="{ height: windowHeight + 'px' }">
		<view class="img-box">
			<image class="header-img" src="../../static/img/title-img.png" mode="aspectFit"></image>
		</view>
		<view class="title">
			工作台
		</view>
		<view class="active-box">
			<view class="item-box">
				<image src="../../static/img/composite-seach.png" mode="aspectFit"></image>
				<text>综合查询</text>
			</view>
			<view class="item-box">
				<image src="../../static/img/plan.png" mode="aspectFit"></image>
				<text>随访计划</text>
			</view>
			<view class="item-box">
				<image src="../../static/img/statistics.png" mode="aspectFit"></image>
				<text>随访统计</text>
			</view>
			<view class="item-box">
				<image src="../../static/img/work-case.png" mode="aspectFit"></image>
				<text>今日工作概况</text>
			</view>
			<view class="item-box">
				<image src="../../static/img/work-search.png" mode="aspectFit"></image>
				<text>工作情况查询</text>
			</view>
			<view class="item-box">
				<image src="../../static/img/user-center.png" mode="aspectFit"></image>
				<text>个人中心</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				windowHeight:0,
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
		padding: 0 20PX;
		display: flex;
		flex-direction: column;
		.img-box {
			flex: 1.5;
			flex-basis: 0;
			.header-img {
				width: 100%;
				height: 150rpx;
				margin-top: 20rpx;
			}
		}
		.title{
			flex: 1;
			flex-basis: 0;
			font-size: 60rpx;
			text-align: center;
			background-color: #b6e2c5;
			padding: 20rpx 0;
		}
		.active-box{
			flex: 7.5;
			flex-basis: 0;
			width: 100%;
			display: flex;
			flex-wrap: wrap;
			align-content: flex-start;
			.item-box {
				flex: 1;
				flex-basis: 0;
				width: 33.3%;
				border: 1px solid $uni-border-color;
				height: 300rpx;
				min-width: 33.3%;
				max-width: 33.3%;
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: center;
				image{
					width: 100rpx;
					height: 100rpx;
					margin-bottom: 10rpx;
				}
				
			}
		}
	}
</style>
