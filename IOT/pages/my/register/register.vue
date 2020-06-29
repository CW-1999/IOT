<!-- 注册页面 06281352 BY CW -->
<!-- 修改者 	修改时间 	修改内容 -->
<template>
	<view class="register">
		<!-- 返回图标 start -->
			<image src="/static/public-icon/return.png" @click="Return"></image>
		<!-- 返回图标 end -->
		<!-- 标题 start -->
			<view class="title">
				注册
				<view>
					Sign up
				</view>
			</view>
		<!-- 标题 end -->
		
		
		<!-- 表单 start -->
			<form @submit="formSubmit" @reset="formReset">
				<!-- 账号 start -->
					<view class="box1">
						<!-- 输入框 start -->
							<input name="account" maxlength="12" placeholder-class="placeholder1" placeholder="请输入账号" />
						<!-- 输入框 end -->
					</view>
				<!-- 账号 end -->
				<!-- 密码 start -->
					<view class="box2">
						<!-- 输入框 start -->
							<input password="true" name="password" maxlength="12" placeholder-class="placeholder2" placeholder="请输入密码" />
						<!-- 输入框 end -->
					</view>
					<view class="box2">
						<!-- 输入框 start -->
							<input password="true" name="passwordAffirm" maxlength="12" placeholder-class="placeholder2" placeholder="确认密码" />
						<!-- 输入框 end -->
					</view>
				<!-- 密码 end -->
				
				<!-- 登录 start -->
					<button form-type="submit">
						注册
					</button>
				<!-- 登录 end -->
			</form>
		<!-- 表单 end -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		methods:{
			// 返回上一级界面
			Return(){
				uni.navigateBack({
					
				})
			},
			// 提交表单
			formSubmit(e) {
				uni.showLoading({
					title:"注册中"
				})
				console.log('form发生了submit事件，携带数据为：' + JSON.stringify(e.detail.value))
			    var formdata = e.detail.value
				console.log(formdata)
				if(formdata.password!=formdata.passwordAffirm)
				{
					console.log("两次输入的密码不一致！")
				}
				else{
					uni.request({
					    url: 'http://121.37.199.83:8888/register/register', //仅为示例，并非真实接口地址。
					    data: {
					        a: formdata.account,
							b:formdata.password
					    },
					    success: (res) => {
					        console.log(res)
							uni.hideLoading()
							uni.showToast({
							    title: '注册成功！',
							    duration: 1000
							});
							setTimeout(()=>{
								uni.navigateBack({
									
								})
							},1000)
					    }
					})
				}
			},
		}
	}
</script>

<style lang="stylus">
	Flex(){
		display flex
		flex-direction column
		align-items center
	}
	Font(a,b,c,d,e=center){
		font-size a
		color b
		line-height c
		font-weight d
		text-align e
		font-family Source Han Sans CN
	}
	.register{
		width 750upx
		height 100vh
		background linear-gradient(30deg,rgba(255, 255, 255, 1.0) 25%,rgba(95, 244, 251, 1.0) 100%)
		Flex()
		image{
			position absolute
			top 32upx
			left 32upx
			width 64upx
			height 64upx
		}
		.title{
			Font(44upx,#000000,44upx,bold)
			margin-top 20upx
			view{
				Font(28upx,#7f7f7f,28upx,500)
				margin-top 12upx
			}
		}
		.box1{
			margin-top 400upx
			width 688upx
			height 80upx
			background #ffffff;
			border-radius 40upx
			.placeholder1{
				Font(32upx,#7f7f7f,80upx,500)
			}
			input{
				Font(32upx,#000000,80upx,500)
				height 80upx
			}
		}
		.box2{
			margin-top 36upx
			width 688upx
			height 80upx
			background #ffffff;
			border-radius 40upx
			.placeholder2{
				Font(32upx,#7f7f7f,80upx,500)
			}
			input{
				Font(32upx,#000000,80upx,500)
				height 80upx
			}
		}
		button{
			height 80upx
			width 688upx
			background #007AFF;
			border-radius 40upx
			Font(32upx,#FFFFFF,80upx,bold)
			margin-top 120upx
			letter-spacing 48upx
			text-indent 1.5em
		}
	}
</style>
