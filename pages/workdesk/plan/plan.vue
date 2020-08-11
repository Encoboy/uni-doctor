<template>
	<view class="hospital-box" :style="{ height: windowHeight + 'px' }">
		<view class="header-img-box">
			<image src="@/static/img/title-img.png" mode="aspectFit"></image>
		</view>
		<view class="header-big-title">
			随访计划
		</view>
		<view class="search-box">
			<u-select v-model="timeShow" :list="timeList" @confirm="timeConfirm"></u-select>
			<u-select v-model="statusShow" :list="statusList" @confirm="statusConfirm"></u-select>
			<u-select v-model="typeShow" :list="typeList" @confirm="typeConfirm"></u-select>
			<view class="item-box">
				<text>随访时间：</text>
				<view class="selected" @click="timeShow = true">
					<text>{{selectTime}}</text>
					<u-icon name="arrow-down-fill" color="black" size="28"></u-icon>
				</view>
			</view>
			<view class="item-box">
				<text>处理状态：</text>
				<view class="selected" @click="statusShow = true">
					<text>{{selectStatus}}</text>
					<u-icon name="arrow-down-fill" color="black" size="28"></u-icon>
				</view>
			</view>
			<view class="item-box">
				<text>随访类型：</text>
				<view class="selected" @click="typeShow = true">
					<text>{{selectType}}</text>
					<u-icon name="arrow-down-fill" color="black" size="28"></u-icon>
				</view>
			</view>
			<input type="text" value="" placeholder="请输入姓名和身份证" placeholder-style="font-size:20rpx"/>
			<view class="mini-btn">
				查询
			</view>
		</view>
		<view class="table-box">
			<scroll-view scroll-x="true" scroll-y="true" >
				<view class="scroll-box">
					<u-table>
						<u-tr>
							<u-th>序号</u-th>
							<u-th>姓名</u-th>
							<u-th>性别</u-th>
							<u-th width="25%">证件号码</u-th>
							<u-th>民族</u-th>
							<u-th width="15%">联系电话</u-th>
							<u-th width="10%">主治医生</u-th>
							<u-th width="25%">操作</u-th>
						</u-tr>
						<u-tr>
							<u-td>1</u-td>
							<u-td>
								<text style="color: #007AFF;">王五</text>
							</u-td>
							<u-td>男</u-td>
							<u-td width="25%">452226199840125402</u-td>
							<u-td>壮</u-td>
							<u-td width="15%">18877495623</u-td>
							<u-td width="10%">
								<text style="color: #007AFF;">李科</text>
							</u-td>
							<u-td width="25%">
								<view class="action">
									<view class="action-btn look-info">
										调查信息
									</view>
									<view class="action-btn add-plan">
										新增随访计划
									</view>
								</view>
							</u-td>
						</u-tr>
					</u-table>
				</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				windowHeight:0,
				timeShow: false,
				statusShow:false,
				typeShow:false,
				selectTime:'全部',
				selectStatus:'全部',
				selectType:'全部',
				timeList: [
					{
						value: '0',
						label: '全部'
					},
					{
						value: '1',
						label: '已到期'
					},
					{
						value: '2',
						label: '未到期'
					}
				],
				statusList: [
					{
						value: '0',
						label: '全部'
					},
					{
						value: '1',
						label: '未处理'
					},
					{
						value: '2',
						label: '已处理'
					}
				],
				typeList: [
					{
						value: '0',
						label: '全部'
					},
					{
						value: '1',
						label: '固定生成'
					},
					{
						value: '2',
						label: '回访跟踪'
					},
					{
						value:'3',
						label:'人工生成'
					}
				],
				selectTime:'全部',
				selectStatus:'全部',
				selectType:'全部'
			}
		},
		onLoad() {
			const res = uni.getSystemInfoSync();
			this.windowHeight = res.windowHeight;
		},
		methods: {	
			timeConfirm(e) {
				console.log(e);
				let time = e[0].label;
				this.selectTime = time;
			},
			statusConfirm(e){
				console.log(e);
				let status = e[0].label;
				this.selectStatus = status;
			},
			typeConfirm(e){
				console.log(e);
				let type = e[0].label;
				this.selectType = type;
			}
		}
	}
</script>

<style lang="scss">
.hospital-box{
	.search-box {
		flex: 2;
		flex-basis: 0;
		display: flex;
		flex-direction: row;
		align-items: center;
		flex-wrap: wrap;
		.item-box {
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			align-items: center;
			margin-right: 20rpx;
			.selected{
				border: 1px solid $uni-border-color;
				padding: 5rpx 3rpx;
				width: 160rpx;
				display: flex;
				flex-direction: row;
				justify-content: space-around;
			}
		}
		input{
			border: 1px solid $uni-border-color;
			width: 295rpx;
			height: 50rpx;
			margin-right: 20rpx;
		}
	}
	.table-box{
		flex:6.5;
		flex-basis: 0;
		padding-top: 100rpx;
		.scroll-box {
			width: 220%;
			height: 425rpx ;
			.action{
				display: flex;
				flex-direction: row;
				justify-content: space-around;
				.action-btn{
					color: white;
					height: 60rpx;
					text-align: center;
					line-height: 60rpx;
				}
				.look-info{
					background-color: #00cc66;
					width: 150rpx;
					border-radius: 150rpx;
				}
				.add-plan {
					background-color: #9966cc;
					width: 190rpx;
					border-radius: 190rpx;
				}
			}
		}
	}
}
</style>

