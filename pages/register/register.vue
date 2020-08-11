<template>
	<view class="hospital-box" :style="{ height: windowHeight + 'px' }">
		<view class="header-img-box">
			<image src="../../static/img/title-img.png" mode="aspectFit"></image>
		</view>
		<view class="motto-box">
			<image src="../../static/img/motto-img.png" mode="aspectFit"></image>
		</view>
		<view class="form-box">
			<view class="text">
				实名注册
			</view>
			 <form class="form" @submit="formSubmit" @reset="formReset">
					 <view class="head-photo">
						<image src="../../static/img/head-photo.png" mode="aspectFit"></image>
					 </view>
					 <input class="user" name="user"  placeholder="姓名" placeholder-style="color:#d9d9d9"/>
					 <input  class="psw" name="psw" password  placeholder="6-16位密码,区分大小写" placeholder-style="color:#d9d9d9"/>
					 <input class="anain-psw" name="again-pws" password  placeholder="确认密码" placeholder-style="color:#d9d9d9"/>
					 <view class="phone">
					 	<view class="code">
					 		+ 86
					 	</view>
						<input name="phone" placeholder="11位手机号" placeholder-style="color:#d9d9d9"/>
					 </view>
					 <view class="verification-code">
					 	<input name='verificationCode' placeholder="输入验证码" placeholder-style="color:#d9d9d9" />
						<view class="get-verificationCode">
							获取验证码
						</view>
					 </view>
					 <view class="accounted">
					 	使用已有账户登录
					 </view>
					 <view class="form-btn">
						 <button class="submit" form-type="submit">确认</button>
						 <button class="register reg" form-type="reset">取消</button>
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
			.text {
				font-size: 80rpx;
				font-weight: 500;
				color: #ff3300;
				text-align: center;
			}
			.form {
				display: flex;
				flex-direction: column;
				.head-photo {
					text-align: center;
					image{
						width: 130rpx;
						height: 130rpx;
					}
				}
				// input输入框
				.user,.psw,.anain-psw {
					width: 96%;
					height: 70rpx;
					border: 1px solid #d9d9d9;
					border-radius: 15rpx;
					padding-left: 20rpx;
					margin-bottom: 30rpx;
				}
				.phone {
					display: flex;
					flex-direction: row;
					border: 1px solid #d9d9d9;
					width: 100%;
					height: 70rpx;
					border-radius: 15rpx;
					margin-bottom: 30rpx;
					.code {
						flex: 2;
						flex-basis: 0;
						height: 70rpx;
						border-right: 1px solid #d9d9d9 ;
						text-align: center;
						line-height: 70rpx;
					}
					input{
						flex: 8;
						flex-basis: 0;
						height: 70rpx;
						padding-left: 20rpx;
					}
				}
				.verification-code {
					display: flex;
					flex-direction: row;
					width: 100%;
					height: 70rpx;
					margin-bottom: 30rpx;
					input {
						flex: 6;
						flex-basis: 0;
						height: 70rpx;
						padding-left: 20rpx;
						border: 1px solid #d9d9d9 ;
						border-radius: 15rpx;
						margin-right: 15rpx;
					}
					.get-verificationCode {
						flex: 4;
						flex-basis: 0;
						height: 70rpx;
						border: 1px solid #d9d9d9 ;
						text-align: center;
						line-height: 70rpx;
						border-radius: 15rpx;
					}
					
				}
				.accounted {
					color: blue;
					margin-top: 40rpx;
					margin-bottom: 15rpx;
					text-align: end;
				}
				// 注册按钮
				.form-btn {
					display: flex;
					flex-direction: row;
					justify-content: space-around;
					.submit,.register {
						width: 300rpx;
						height: 80rpx;
						font-size: 34rpx;
						background-color: #66ff66;
						border: none;
						border-radius: 480rpx;
						color: white;
						line-height: 80rpx;
					}
					.reg{
						background-color: #cccccc;
						border: none;
						color: white;
					}
				}
			}
		}
	}
</style>

