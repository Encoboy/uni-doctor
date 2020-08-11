<template>
	<view class="hospital-box" :style="{ height: windowHeight + 'px' }">
		<view class="header-img-box">
			<image src="../../../static/img/title-img.png" mode="aspectFit"></image>
		</view>
		<view class="header-title">
			王五
		</view>
		<view class="scroll-box" >
			<!-- 用戶信息 -->
			<user-info :reUserInfo="userInfoData"></user-info>
			<!-- 门诊记录 -->
			<view class="outpatient">
				<view class="inhabit-title">
					<text>门诊记录</text>
				</view>
				<scroll-view class="scroll-view_H" scroll-x="true">
					<view class="table-box">
					<view class="content-box">
						<view class="header-row">
							<view class="header-row-title">
								门诊记录
							</view>
							<view class="action th-action" >
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
				<view class="inhabit-title">
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
				<view class="inhabit-title">
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
				<view class="inhabit-title">
					<text>监护记录</text>
				</view>
				<line-chart-list></line-chart-list>
			</view>
		</view>
		
	</view>
</template>

<script>
	import UserInfo from '@/components/userinfo/userinfo.vue';
	import LineChartList from '../components/lineChartList.vue';
	export default {
		components: {
			'user-info':UserInfo,
			'line-chart-list':LineChartList
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
				],
				userInfoData:{
					'name':'王五',
					'idCard':'45636856397848',
					'sex':'男',
					'marryStatus':'已婚',
					'nation':'民族',
					'work':'自由職業',
					'boold':'A',
					'rhBoold':'未知',
					'drugAllergy':'無',
					"phone":'13664644444',
					"location":'广西南宁市青秀区东葛路'
				}
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
		},
		onLoad() {
			const res = uni.getSystemInfoSync();
			this.windowHeight = res.windowHeight;
		}
	}
</script>

<style lang="scss">
	.hospital-box {
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
			// 门诊记录 住院記錄
			.outpatient,.inHospital {
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
						.th-action{
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
							justify-content: space-around;
							align-items: center;
							width: 70%;
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
		}
	}
</style>
