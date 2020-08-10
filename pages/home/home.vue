<template>
	<view class="hospital-box" :style="{ height: windowHeight + 'px' }">
		<view class="img-box">
			<image class="header-img" src="../../static/img/title-img.png" mode="aspectFit"></image>
		</view>
		<view class="header-title">
			总体情况
		</view>
		<view class="select-date">
			<text class="date-title">选择日期:</text>
			<view class="date-box"  @click="show = true">
				<text>{{startDate}}</text>
				<text>~</text>
				<text>{{endDate}}</text>
				<image src="../../static/img/datebtn.png" mode="aspectFit"></image>
			</view>
			<u-calendar v-model="show" :mode="mode" @change="change"></u-calendar>
		</view>
		<view class="table-box">
			<u-table class="table-title">
				<u-tr>
					<u-th>姓名</u-th>
					<u-th>血糖</u-th>
					<u-th>血压</u-th>
					<u-th>心率</u-th>
					<u-th>操作</u-th>
				</u-tr>
			</u-table>
			<u-table class="table-content">
				<u-tr>
					<u-td><text class="name">王五</text></u-td>
					<u-td><text @click="goDataVisualization">50</text></u-td>
					<u-td><text @click="goDataVisualization">40</text></u-td>
					<u-td><text @click="goDataVisualization">30</text></u-td>
					<u-td>
						<view class="action">
							反馈
						</view>
					</u-td>
				</u-tr>
			</u-table>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				windowHeight:0,
				show: false,
				mode: 'range',
				startDate:'',
				endDate:'',
				key:0,
			}
		},
		onLoad() {
			const res = uni.getSystemInfoSync();
			this.windowHeight = res.windowHeight;
		},
		methods: {
			change(e) {
				console.log(e);
				this.startDate = e.startDate;
				this.endDate = e.endDate;
			},
			goDataVisualization:function(){
				uni.navigateTo({
					url:'/pages/home/dataVisualization/dataVisualization'
				})
			}
			
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
		.header-title {
			flex: 1;
			flex-basis: 0;
			font-size: 80rpx;
			text-align: center;
		}
		// 选择日期
		.select-date{
			flex: 1;
			flex-basis: 0;
			display: flex;
			flex-direction: row;
			.date-title {
				flex: 2;
				flex-basis: 0;
				text-align: center;
				height: 60rpx;
				line-height: 60rpx;
			}
			.date-box {
				flex: 8;
				flex-basis: 0;
				display: flex;
				flex-direction: row;
				justify-content: space-around;
				border: 1px solid $uni-border-color;
				height: 60rpx;
				align-items: center;
				border-radius: 10rpx;
				image {
					width: 50rpx;
					height: 50rpx;
				}
			}
			
		}
		.table-box {
			flex: 6.5;
			flex-basis: 0;
			border: 1px solid black;
			display: flex;
			flex-direction: column;
			.table-title{
				flex: 1;
				flex: 0;
			}
			.table-content{
				flex: 8;
				flex-basis: 0;
				overflow-y: scroll;
				.name{
					color:blue;
				}
				.action {
					color: white;
					background-color: #169bd5;
					width: 80rpx;
					height: 40rpx;
					border-radius: 10rpx;
					margin: auto;
				}
			}
		}
	}
</style>
