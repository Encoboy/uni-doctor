<template>
	<view class="tabbar">
		<image :src="home?selectHome:notSelectHome" @click="cutHome" mode="aspectFit"></image>
		<image :src="work?selectWork:notSelectWork" @click="cutWork" mode="aspectFit"></image>
		<image :src="chat?selectChat:notSelectChat" @click="cutChat" mode="aspectFit"></image>
	</view>
</template>

<script>
	export default {
		data(){
			return {
				home:true,
				work:false,
				chat:false,
				selectHome:'../../static/img/home-select.png',
				selectWork:'../../static/img/work-select.png',
				selectChat:'../../static/img/chat-select.png',
				notSelectHome:'../../static/img/home-notselect.png',
				notSelectWork:'../../static/img/work-notselect.png',
				notSelectChat:'../../static/img/chat-notselect.png'
			}
		},
		onLoad(options) {
			console.log('ss:',options)
			let cut = options.type;
			console.log(cut)
		},
		methods:{
			cutHome(){
				// 页面跳转的话就重新渲染了，所以还是home
				this.home = true;
				this.work = false;
				this.chat = false;
				let cutPage = {
					isHome:this.home,
					isWork:this.work,
					isChat:this.chat
				}
				let type = JSON.stringify(cutPage)
				uni.navigateTo({
					url:`/pages/home/home?type=${type}`
				})
			},
			cutWork(){
				this.home = false;
				this.work = true;
				this.chat = false;
				let cutPage = {
					isHome:this.home,
					isWork:this.work,
					isChat:this.chat
				}
				let type = JSON.stringify(cutPage)
				uni.navigateTo({
					url:`/pages/workdesk/workdesk?type=${type}`
				});
			},
			cutChat(){
				this.home = false;
				this.work = false;
				this.chat = true;
				// uni.navigateTo({
				// 	url:'/pages/conversations/conversations'
				// });
			}
		}
	}
</script>

<style lang="scss">
	.tabbar{
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		padding: 10rpx;
		image {
			width: 80rpx;
			height: 80rpx;
		}
	}
</style>
