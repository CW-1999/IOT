<!-- 个人中心页面 06271540 BY CW -->
<!-- 修改者 	修改时间 	修改内容 -->
<template>
	<view class="my">
		<!-- 未登录下的界面 start -->
			<view class="" v-if="!isLogin">
				<!-- 头像+昵称 Box start -->
					<view class="Box">
						<!-- 头像+昵称 Box end -->
						<!-- 头像 start -->
							<view class="head-portrait">
									
							</view>
						<!-- 头像 end -->
						<!-- 昵称 start -->
							<view class="nikename">
									未登录
							</view>
						<!-- 昵称 end -->
					</view>
			</view>
		<!-- 未登陆的界面 end -->
		
		<!-- 登陆后的界面 start -->
			<view class="" v-else>
				
			</view>
		<!-- 登陆后的界面 end -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				isLogin:false
			};
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
	.my{
		height calc(100vh - 188upx)
		/* #ifdef MP */
		height 100vh
		/* #endif */
		width 750upx
		
		Flex()
		.Box{
			background linear-gradient(to right,rgba(30, 115, 242, 1.0) 33%,rgba(95, 244, 251, 1.0) 100%)
			width 750upx
			Flex()
			.head-portrait{
				width 128upx
				height 128upx
				border-radius 50%
				background #FFFFFF;
				overflow hidden
				margin-top 80upx
			}
			.nikename{
				margin-top 32upx
				margin-bottom 32upx
				Font(32upx,#FFFFFF,32upx,bold)
			}
		}
	}
</style>
