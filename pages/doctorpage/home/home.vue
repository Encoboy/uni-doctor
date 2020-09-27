<template>
	<view class="hospital-box" :style="{ height: windowHeight + 'px' }">
		<view class="header-img-box">
			<image src="@/static/img/title-img.png" mode="aspectFit"></image>
		</view>
		<view class="header-big-title" >
			总体情况
		</view>
		<sing-date></sing-date>
		<view class="table-box">
			<u-table class="table-title">
				<u-tr>
					<block v-for="(item,index) in tabelThArr" :key="index">
						<u-th>{{item}}</u-th>
					</block>
				</u-tr>
			</u-table>
			<u-table class="table-content">
				<block v-for="(item,index) in tableUtdContentArr" :key="index">
					<u-tr>
						<u-td><text class="name" @click="goInhabitantInfo(item.name)">{{item.name}}</text></u-td>
						<u-td><text @click="goDataVisualization">{{item.xuetang}}</text></u-td>
						<u-td><text @click="goDataVisualization">{{item.xueya}}</text></u-td>
						<u-td><text @click="goDataVisualization">{{item.xinlv}}</text></u-td>
						<u-td>
							<view class="mini-btn" @click="goFeedback">
								反馈
							</view>
						</u-td>
					</u-tr>
				</block>
			</u-table>
		</view>
		<doc-tabbar :tabbarType="tabbarType" :unreadTotal="unreadTotal"></doc-tabbar>
	</view>
</template>

<script>
	import SelectDate from '@/components/selectDate/selectDate.vue';
	import SingleDate from '@/components/selectDate/singleDate.vue';
	import DocTabbar from '@/components/docTabbar/docTabbar.vue';
	export default {
		components:{
			'select-date':SelectDate,
			'sing-date':SingleDate,
			'doc-tabbar':DocTabbar,
		},
		data() {
			return {
				windowHeight:0,
				unreadTotal:0,
				tabbarType:{
					home:true,
					work:false,
					chat:false,
				},
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
					}
					
				]
				
			}
		},
		onLoad() {
			const res = uni.getSystemInfoSync();
			this.windowHeight = res.windowHeight;
		},
		onShow() {
			console.log('sha')
		},
		methods: {
			goDataVisualization(){
				uni.navigateTo({
					url:'/pages/doctorpage/home/dataVisualization/dataVisualization'
				})
			},
			goInhabitantInfo(name){
				uni.navigateTo({
					url:`/pages/doctorpage/home/inhabitantInfo/inhabitantInfo?name=${name}`
				})
			},
			goFeedback(){
				uni.navigateTo({
					url:'/pages/doctorpage/home/feedback/feedback'
				})
			},
		}
	}
</script>

<style lang="scss">
	.hospital-box{
		.table-box {
			flex: 6.5;
			flex-basis: 0;
			display: flex;
			flex-direction: column;
			margin-top: 30rpx;
			.table-content{
				overflow-y: scroll;
				.name{
					color:blue;
				}
			}
		}
	}
</style>
