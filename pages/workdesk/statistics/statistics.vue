<template>
	<view class="hospital-box" :style="{ height: windowHeight + 'px' }">
		<view class="header-img-box">
			<image src="@/static/img/title-img.png" mode="aspectFit"></image>
		</view>
		<view class="header-big-title">
			总体情况
		</view>
		<!-- 选择日期 -->
		<select-date></select-date>
		<view class="radio-box">
			<u-radio-group v-model="value" @change="radioGroupChange">
				<u-radio 
					@change="radioChange" 
					v-for="(item, index) in list" :key="index" 
					:name="item.name"
					:disabled="item.disabled"
				>
					{{item.name}}
				</u-radio>
			</u-radio-group>
		</view>
		<view class="chart-box">
			<view>
				<histogram-chart :dataAs="histogramData" canvasId="ht0" />
				<view style="text-align: center;line-height: 40px;">柱状图histogram Number</view>
			</view>
		</view>
	</view>
</template>

<script>
	import SelectDate from '@/components/selectDate/selectDate.vue';
	import HistogramCharts from '@/components/stan-ucharts/HistogramChart.vue'
	export default {
		components:{
			'select-date':SelectDate,
			'histogram-chart':HistogramCharts,
		},
		data() {
			return {
				windowHeight:0,
				list: [
					{
						name: '柱状图',
						disabled: false
					},
					{
						name: '表格',
						disabled: false
					}
				],
				value: '柱状图',
				histogramData: {
					//总模板
					categories: ['未到期', '2013', '2014', '2015', '2016', '2017', '2018'],
					series: [
						{
							name: '成交量1', //数据名称
							data: [
								15,
								{
									//(饼图、圆环图、玫瑰图为Number) 数据，如果传入null图表该处出现断点
									value: 20, //	仅针对柱状图有效，主要作用为柱状图显示数值
									color: '#f04864' //仅针对柱状图有效，主要作用为柱状图自定义颜色,可覆盖外框定义主题颜色
								},
								45,
								37,
								43,
								34,
								45
							],
							show: true, //图形显示状态，配合点击图例显示状态，也可默认指定是否显示
							color: '#FF7600', //	图形颜色 不传入则使用系统默认配色方案 即统一柱状图颜色
							textSize: 12 //图形上方标注文字的字体大小
							//如涉及混合图表请看 http://doc.ucharts.cn/1172126
						},
						{
							name: '成交量2',
							data: [
								30,
								{
									value: 40,
									color: '#facc14'
								},
								25,
								14,
								34,
								18,
								20
							]
						}
					]
				},
				histogramData2: {
					//柱状图Compent  //label应为series value 应为
					label: ['2052', '2013', '2014', '2015', '2016', '2017', '2018'],
					value: [
						{
							name: 'labelKey改变',
							data: [0.3, 0.2, 0.5, 0.4, 0.3, 0.1, 0.2]
						}
					]
				},
				histogramData3: {
					//柱状标准图
					categories: ['2013', '2014', '2015', '2016', '2017', '2018'],
					series: [
						{
							name: '类别一',
							data: [35, 36, 31, 33, 13, 34]
						},
						{
							name: '类别二',
							data: [18, 27, 21, 24, 6, 28]
						},
						{
							name: '类别三',
							data: [18, 27, 21, 24, 6, 28]
						}
					]
				},
			}
		},
		onLoad() {
			const res = uni.getSystemInfoSync();
			this.windowHeight = res.windowHeight;
		},
		methods: {
			// 选中某个单选框时，由radio时触发
			radioChange(e) {
				console.log('1'+e);
			},
			// 选中任一radio时，由radio-group触发
			radioGroupChange(e) {
				console.log('2'+e);
			}
		}
	}
</script>

<style lang="scss">
	.hospital-box{
		.radio-box{
			flex: 1;
			flex-basis: 0;
			text-align: end;
		}
		.chart-box {
			flex: 6.5;
			flex-basis: 0;
			border: 1px solid red;
		}
	}
</style>

