<template>
	<view class="hospital-box" :style="{ height: windowHeight + 'px' }">
		<view class="img-box">
			<image class="header-img" src="../../static/img/title-img.png" mode="aspectFit"></image>
		</view>
		<view class="motto-box">
			<image src="../../static/img/motto-img.png" mode="aspectFit"></image>
		</view>
		<view class="form-box">
			<view class="login-text">
				登  录
			</view>
			 <form class="form" @submit="formSubmit" @reset="formReset">
					<view class="login-user">
						 <image src="../../static/img/icon-user.png" mode=""></image>
						 <input name="user" placeholder="请输入用户名" />
					 </view>
					 <view class="login-psw">
					 	<image src="../../static/img/icon-psw.png" mode=""></image>
						<input password  name="psw" placeholder="请输入密码"/>
					 </view>
					 <view class="forget-psw">
					 	忘记密码？
					 </view>
					 <view class="form-btn">
						 <button class="submit" form-type="submit">登录</button>
						 <button class="register reg" form-type="reset">注册</button>
					 </view>
			 </form>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				windowHeight:0,
			}
		},
		onLoad() {
			const res = uni.getSystemInfoSync();
			this.windowHeight = res.windowHeight;
		},
		methods: {
            formSubmit: function(e) {
				console.log('form发生了submit事件，携带数据为：' + JSON.stringify(e.detail.value))
				var formdata = e.detail.value
				uni.showModal({
				    content: '表单数据内容：' + JSON.stringify(formdata),
				    showCancel: false
				});
				uni.switchTab({
					url:'/pages/home/home',
					success() {
						console.log('跳转到首页')
					}
				})

            },
            formReset: function(e) {
                console.log('清空数据')
				uni.navigateTo({
					url:'/pages/register/register',
					success() {
						console.log('跳转到注册页面')
					}
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
		.motto-box {
			flex: 0.5;
			flex-basis: 0;
			image {
				width: 100%;
				height: 84rpx;
			}
		}
		// 登录
		.form-box{
			flex: 8;
			flex-basis: 0;
			width: 100%;
			background-color: #22a77a;
			padding-top: 50rpx;
			.login-text {
				font-size: 60rpx;
				font-weight: 500;
				color: white;
				text-align: center;
			}
			.form {
				display: flex;
				flex-direction: column;
				// input输入框
				.login-user, .login-psw {
					flex: 2;
					flex-basis: 1;
					border: 1px solid black;
					margin: 10PX 20PX 20PX 20PX;
					padding: 5PX 10PX 2PX 10PX;
					background-color: white;
					image {
						width: 80rpx;
						height: 80rpx;
						margin-right: 5PX;
					}
					input {
						display: inline-block;
						height: 80rpx;
						font-size: 30rpx;
					}
				}
				.forget-psw {
					color: #cc6635;
					font-size: 40rpx;
					font-weight: 600;
					margin-left: 40rpx;
					margin-top: -20rpx;
				}
				// 登录按钮
				.form-btn {
					margin: 50PX 0;
					.submit,.register {
						width: 480rpx;
						height: 90rpx;
						font-size: 34rpx;
						background-color: rgba(22, 155, 213, 1);
						border: none;
						border-radius: 480rpx;
						color: white;
						line-height: 90rpx;
					}
					.reg{
						background-color: rgba(255, 255, 255, 1);
						border:1PX solid rgba(0, 102, 255, 1);
						color: rgba(0, 102, 255, 1);
						margin-top: 20PX;
					}
				}
			}
		}
	}
</style>
