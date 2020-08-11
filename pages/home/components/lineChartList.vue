<template>
	<view>
		<view class="select-date">
			<text class="date-title">选择日期:</text>
			<view class="date-box"  @click="show = true">
				<text>{{startDate}}</text>
				<text>~</text>
				<text>{{endDate}}</text>
				<image src="@/static/img/datebtn.png" mode="aspectFit"></image>
			</view>
			<u-calendar v-model="show" :mode="mode" @change="change"></u-calendar>
		</view>
		<view class="table-box">
			<view class="unit">
				<view class="name">
					血糖
				</view>
				<view class="mmhg">
					单位mmhg
				</view>
			</view>
			<view class="line">
				<line-chart canvasId="index_line_2" :dataAs="lineData2" />
			</view>
			<view class="unit">
				<view class="name">
					血压
				</view>
				<view class="mmhg">
					单位mmhg
				</view>
			</view>
			<view class="line">
				<line-chart canvasId="index_line_2" :dataAs="lineData2" />
			</view>
			<view class="unit">
				<view class="name">
					心率
				</view>
				<view class="mmhg">
					单位mmhg
				</view>
			</view>
			<view class="line">
				<line-chart canvasId="index_line_2" :dataAs="lineData2" />
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
				show: false,
				mode: 'range',
				startDate:'',
				endDate:'',
				key:0,
				color:'blue',
				lineData2: {
					//数字的图--折线图数据
					categories: ['1', '2', '3', '4', '5', '6'],
					series: [
						{ name: '实时', data: [35000, 80000, 25000, 37000, 40000, 20000] },
					]
				},
			}
		},
		onLoad() {
		},
		methods: {
			change(e) {
				console.log(e);
				this.startDate = e.startDate;
				this.endDate = e.endDate;
			}
		}
	}
</script>

<style lang="scss">
	/* 选择日期 */
	.select-date{
		flex: 0.5;
		flex-basis: 0;
		display: flex;
		flex-direction: row;
		margin-top: 20rpx;
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
	/* 数据展示 */
	.table-box {
		flex: 6.5;
		flex-basis: 0;
		display: flex;
		flex-direction: column;
		overflow-y: scroll;
		.unit{
			margin-left: 25rpx;
			.name{
				font-size: 40rpx;
				font-weight: 600;
				margin-top: 50rpx;
				color: red;
			}
			.mmhg{
				font-size: 30rpx;
				color: lightgray;
			}
		}
	}
</style>
