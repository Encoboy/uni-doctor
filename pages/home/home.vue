<template>
	<view class="hospital-box" :style="{ height: windowHeight + 'px' }">
		<view class="header-img-box">
			<image src="../../static/img/title-img.png" mode="aspectFit"></image>
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
					<block v-for="(item,index) in tabelThArr" :key="index">
						<u-th>{{item}}</u-th>
					</block>
				</u-tr>
			</u-table>
			<u-table class="table-content">
				<block v-for="(item,index) in tableUtdContentArr">
					<u-tr>
						<u-td><text class="name" @click="goInhabitantInfo(item.name)">{{item.name}}</text></u-td>
						<u-td><text @click="goDataVisualization">{{item.xuetang}}</text></u-td>
						<u-td><text @click="goDataVisualization">{{item.xueya}}</text></u-td>
						<u-td><text @click="goDataVisualization">{{item.xinlv}}</text></u-td>
						<u-td>
							<view class="action" @click="goFeedback">
								反馈
							</view>
						</u-td>
					</u-tr>
				</block>
			</u-table>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				windowHeight:0,
				show: false,
				mode: 'range',
				startDate:'',
				endDate:'',
				tabelThArr:[
					'姓名',
					'血糖',
					'血压',
					'心率',
					'操作',
				],
				tableUtdContentArr:[
					{
						name:'王五',
						xuetang:'50',
						xueya:'40',
						xinlv:'30'
					},
					{
						name:'张三',
						xuetang:'60',
						xueya:'40',
						xinlv:'30'
					},
				]
				
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
			},
			goInhabitantInfo:function(options){
				console.log(options)
				uni.navigateTo({
					url:'/pages/home/inhabitantInfo/inhabitantInfo?name=options'
				})
			},
			goFeedback:function(){
				uni.navigateTo({
					url:'/pages/home/feedback/feedback'
				})
			},
			
		}
	}
</script>

<style lang="scss">
	.hospital-box{
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
