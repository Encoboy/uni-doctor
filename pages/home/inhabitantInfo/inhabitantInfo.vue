<template>
	<view class="user-center" :style="{ height: windowHeight + 'px' }">
		<view class="img-box">
			<image class="header-img" src="../../../static/img/title-img.png" mode="aspectFit"></image>
		</view>
		<view class="header-title">
			王五
		</view>
		<view class="scroll-box" >
			<view class="userinfo">
				<view class="title">
					<text>基本信息</text>
				</view>
				<view class="info">
					<view class="left">
						姓名：王五
					</view>
					<view class="right">
						身份证号：<text>452225199812135264</text>
					</view>
				</view>
				<view class="info">
					<view class="left">
						性别：男
					</view>
					<view class="right">
						婚姻状况：已婚
					</view>
				</view>
				<view class="info">
					<view class="left">
						民族：汉
					</view>
					<view class="right">
						职业：自由职业
					</view>
				</view>
				<view class="info">
					<view class="left">
						血型：A
					</view>
					<view class="right">
						RH血型：未知
					</view>
				</view>
				<view class="info">
					<view class="left">
						药物过敏：无
					</view>
				</view>
				<view class="info">
					<view class="left">
						联系电话：1366464444444
					</view>
				</view>
				<view class="info">
					<view class="left">
						家庭地址：广西南宁市青秀区东葛路
					</view>
				</view>
			</view>
			<!-- 门诊记录 -->
			<view class="outpatient">
				<view class="title">
					<text>门诊记录</text>
				</view>
				<scroll-view class="scroll-view_H" scroll-x="true">
					<view class="table-box">
					<view class="content-box">
						<view class="header-row">
							<view class="header-row-title">
								门诊记录
							</view>
							<view class="action">
								操作
							</view>
						</view>
						<view class="th-row">
							<view class="th-row-title">
								2019-02-20  肺部感染
							</view>
							<view class="action th-action">
								<view>病历</view>
								<view>处方</view>
								<view>化验</view>
								<view>PACS</view>
							</view>
						</view>
						</view>
					</view>
				</scroll-view>
			</view>
			<!-- 住院记录 -->
			<view class="inHospital">
				<view class="title">
					<text>住院记录</text>
				</view>
				<scroll-view class="scroll-view_H" scroll-x="true">
					<view class="table-box">
						<view class="content-box">
							<view class="header-row">
								<view class="header-row-title">
									门诊记录
								</view>
								<view class="action th-action">
									操作
								</view>
							</view>
							<view class="th-row">
								<view class="th-row-title">
									2019-02-20  住院 呼吸病
								</view>
								<view class="action th-action">
									<view>入院记录</view>
									<view>长期医嘱</view>
									<view>临时医嘱</view>
									<view>检查结果</view>
									<view>PACS</view>
									<view>出院小结</view>
								</view>
							</view>
							</view>
					</view>
				</scroll-view>
			</view>
			<!-- 用药记录 -->
			<view class="pharmacy">
				<view class="title">
					<text>用药记录</text>
				</view>
				<scroll-view class="scroll-view_H" scroll-x="true">
					<view class="table-box">
						<view class="content-box">
							<view class="pharmacy-type">
								处方类型：西药处方日期：2016-05-31 15:37:08 诊断:急性冠周炎医疗机构：广西壮族自治区江滨医院
							</view>
								<u-table>
									<u-tr>
										<block v-for="(item,index) in pharmacyHeadList" :key="index">
											<u-th>{{item}}</u-th>
										</block>
									</u-tr>
									<u-tr  v-for="(item,index) in pharmacyContentArr" :key="index">
										<block v-for="(name,id) in item" :key="id">
											<u-td>{{name}}</u-td>
										</block>
									</u-tr>
								</u-table>
						</view>
					</view>
				</scroll-view>
			</view>
			<view class="guardianship">
				<view class="title">
					<text>监护记录</text>
				</view>
				<view class="select-date">
					<text class="date-title">选择日期:</text>
					<view class="date-box"  @click="show = true">
						<text>{{startDate}}</text>
						<text>~</text>
						<text>{{endDate}}</text>
						<image src="../../../static/img/datebtn.png" mode="aspectFit"></image>
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
		</view>
		
	</view>
</template>

<script>
	import LineChart from '@/components/stan-ucharts/LineChart.vue';
	export default {
		components: {
			LineChart,
		},
		data(){
			return {
				windowHeight:0,
				pharmacyHeadList:[
					'药品名称',
					'药品数量',
					'数量单位',
					'一次剂量',
					'剂量单位',
					'给药途径',
					'药品用法',
					'用药天数',
					'每日次数'
				],
				pharmacyContentArr:[
					[
						'药品名称1',
						'药品数量1',
						'数量单位1',
						'一次剂量1',
						'剂量单位1',
						'给药途径1',
						'药品用法1',
						'用药天数1',
						'每日次数1'
					],
					[
						'药品名称2',
						'药品数量2',
						'数量单位2',
						'一次剂量2',
						'剂量单位2',
						'给药途径2',
						'药品用法2',
						'用药天数2',
						'每日次数2'
					]
				],
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
		methods:{
			addEquipment:function(){
				uni.navigateTo({
					url:'/pages/userCenter/component/addEquipment',
				})
			},
			editUserInfo:function(){
				uni.navigateTo({
					url:'/pages/userCenter/component/editUserInfo'
				})
			},
			change(e) {
				console.log(e);
				this.startDate = e.startDate;
				this.endDate = e.endDate;
			}
		},
		onLoad() {
			const res = uni.getSystemInfoSync();
			this.windowHeight = res.windowHeight;
		}
	}
</script>

<style lang="scss">
	.user-center {
		font-size: 60rpx;
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
			flex: 0.8;
			flex-basis: 0;
			font-size: 60rpx;
			text-align: center;
		}
		.scroll-box {
			margin-bottom: 15PX;
			flex: 8;
			flex-basis: 0;
			overflow-y: scroll;
			padding: 0 10rpx;
			// 基本信息
			.userinfo {
				.title {
					width: 100%;
					height: 68rpx;
					background-color: #95cae5;
					display: flex;
					flex-direction: row;
					justify-content: space-between;
					align-items: center;
					border: 1px solid black;
					text {
						color: white;
						font-size: 40rpx;
						margin-left: 5PX;
					}
				}
				.info {
					width: 100%;
					height: 75rpx;
					display: flex;
					flex-direction: row;
					justify-content: space-between;
					color: #0099FF;
					font-size: 35rpx;
					line-height: 75rpx;
					.left {
						flex: 3;
						flex-basis: 1;
						margin-left: 5PX;
						margin-right: 12PX;
					}
					.right {
						flex: 7.5;
						flex-basis: 1;
						margin-right: 5PX;
						text-align: left;
						text {
							font-size: 30rpx;
						}
					}
				}
			}
			// 门诊记录
			.outpatient {
				margin-bottom: 20rpx;
				.title {
					width: 100%;
					height: 68rpx;
					background-color: #95cae5;
					display: flex;
					flex-direction: row;
					justify-content: space-between;
					align-items: center;
					border: 1px solid black;
					text {
						color: white;
						font-size: 40rpx;
						margin-left: 5PX;
					}
				}
				.content-box{
					width: 100%;
					height: 300rpx;
					overflow-y: scroll;
					.header-row {
						display: flex;
						flex-direction: row;
						width: 150%;
						.header-row-title,.action {
							width: 50%;
							height: 60rpx;
							font-size: 30rpx;
							border: 1px solid $uni-border-color;
							text-align: center;
							line-height: 60rpx;
						}
					}

					.th-row {
						display: flex;
						flex-direction: row;
						width: 150%;
						.th-row-title,.action {
							width: 50%;
							height: 80rpx;
							font-size: 30rpx;
							border: 1px solid $uni-border-color;
							text-align: center;
							line-height: 80rpx;
						}
						.th-action {
							display: flex;
							flex-direction: row;
							justify-content: space-between;
							align-items: center;
							view{
								height: 50rpx;
								width: 100rpx;
								background-color: #66ccff;
								text-align: center;
								line-height: 50rpx;
								font-size: 20rpx;
								border-radius: 10rpx;
							}
						}
					}
				}

			}
			// 住院记录
			.inHospital {
				.title {
					width: 100%;
					height: 68rpx;
					background-color: #95cae5;
					display: flex;
					flex-direction: row;
					justify-content: space-between;
					align-items: center;
					border: 1px solid black;
					text {
						color: white;
						font-size: 40rpx;
						margin-left: 5PX;
					}
				}
				.content-box{
					width: 100%;
					height: 300rpx;
					overflow-y: scroll;
					.header-row {
						display: flex;
						flex-direction: row;
						width: 250%;
						.header-row-title,.action {
							width: 30%;
							height: 60rpx;
							font-size: 30rpx;
							border: 1px solid $uni-border-color;
							text-align: center;
							line-height: 60rpx;
						}
						.th-action {
							width: 70%;
						}
					}
					.th-row {
						display: flex;
						flex-direction: row;
						width: 250%;
						.th-row-title,.action {
							width: 30%;
							height: 80rpx;
							font-size: 30rpx;
							border: 1px solid $uni-border-color;
							text-align: center;
							line-height: 80rpx;
						}
						.th-action {
							display: flex;
							flex-direction: row;
							width:70%;
							justify-content: space-between;
							align-items: center;
							view{
								height: 50rpx;
								width: 120rpx;
								background-color: #66ccff;
								text-align: center;
								line-height: 50rpx;
								font-size: 20rpx;
								border-radius: 10rpx;
							}
						}
					}
				}
			}
			// 用药纪律
			.pharmacy {
				.title {
					width: 100%;
					height: 68rpx;
					background-color: #95cae5;
					display: flex;
					flex-direction: row;
					justify-content: space-between;
					align-items: center;
					border: 1px solid black;
					text {
						color: white;
						font-size: 40rpx;
						margin-left: 5PX;
					}
				}
				.content-box{
					width: 200%;
					height: 300rpx;
					overflow-y: scroll;
					.pharmacy-type{
						font-size: 30rpx;
						font-weight: 600;
						margin: 20rpx 0;
					}
				}
			}
			// 监护纪律
			.guardianship{
				.title {
					width: 100%;
					height: 68rpx;
					background-color: #95cae5;
					display: flex;
					flex-direction: row;
					justify-content: space-between;
					align-items: center;
					border: 1px solid black;
					text {
						color: white;
						font-size: 40rpx;
						margin-left: 5PX;
					}
				}
				// 选择日期
				.select-date{
					display: flex;
					flex-direction: row;
					margin: 20rpx 0;
					.date-title {
						flex: 2;
						flex-basis: 0;
						text-align: center;
						height: 60rpx;
						line-height: 60rpx;
						font-size: 30rpx;
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
						font-size: 30rpx;
						image {
							width: 50rpx;
							height: 50rpx;
						}
					}
					
				}
				// 数据展示
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
			}
		}
	}
</style>
