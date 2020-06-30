<!-- 个人中心页面 06271540 BY CW -->
<!-- 修改者 	修改时间 	修改内容 -->
<template>
	<view class="my">
				<!-- 头像+昵称 Box start -->
					<view class="Box">
						<!-- 头像+昵称 Box end -->
						<!-- 头像 start -->
							<view class="head-portrait">
									
							</view>
						<!-- 头像 end -->
						<!-- 昵称 start -->
							<view class="nikename">
									{{nickname}}
							</view>
						<!-- 昵称 end -->
					</view>
				<!-- 头像+昵称 Box end -->
				
				<!-- 工具栏 start -->
					<view class="tool">
						<!-- 单个工具 start -->
							<view class="box" v-for="(item,index) in  tools" :key="index">
								<!-- icon start -->
									<image :src="item.iconpath"></image>
								<!-- icon end -->
								<!-- 名称 start -->
									<view class="name">
										{{item.name}}
									</view>
								<!-- 名称 end -->
							</view>
						<!-- 单个工具 end -->
					</view>
				<!-- 工具栏 end -->
				
				<!-- 功能列表start -->
					<view class="service-list">
						<!-- 单个功能 start -->
							<view class="service" v-for="(item,index) in service" :key="index">
								<!-- icon start -->
									<image :src="item.iconpath"></image>
								<!-- icon end -->
								<!-- 功能名称 start -->
									<view class="name">
										{{item.name}}
									</view>
								<!-- 功能名称 end -->
								<!-- 箭头 start -->
									<view class="arrows">
										>
									</view>
								<!-- 箭头 end -->
								<!-- 分割线 start -->
									<view class="line" v-if="index!=4">
									</view>
								<!-- 分割线 end -->
							</view>
						<!-- 单个功能 end -->
					</view>
				<!-- 功能列表end -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 账号昵称
				nickname:"",
				// 工具列表
				tools:[
					{
						iconpath:"/static/my-icon/ic-log.png",
						name:"操作日志",
						path:""
					},
					{
						iconpath:"",
						name:"工具1",
						path:""
					},
					{
						iconpath:"",
						name:"工具2",
						path:""
					},
				],
				// 功能列表
				service:[
					{
						iconpath:"/static/my-icon/ic-inform.png",
						name:"通知",
						path:""
					},
					{
						iconpath:"/static/my-icon/ic-personal-data.png",
						name:"个人信息",
						path:""
					},
					{
						iconpath:"/static/my-icon/ic-setting.png",
						name:"设置",
						path:""
					},
					{
						iconpath:"/static/my-icon/ic-suggest.png",
						name:"建议反馈",
						path:""
					},
					{
						iconpath:"/static/my-icon/ic-about-us.png",
						name:"关于我们",
						path:""
					},
					]
			};
		},
		onLoad() {
			// console.log(getApp().globalData.isLogin)
			// if(!getApp().globalData.isLogin){
			// 	uni.navigateTo({
			// 		url:"login/login"
			// 	})
			// }
		},
		onShow() {
			this.nickname=getApp().globalData.nickname
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
		background #f3f3f3;
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
				margin-bottom 64upx
				Font(32upx,#FFFFFF,32upx,bold)
			}
		}
		.tool{
			width 688upx
			height 200upx
			background #ffffff;
			position relative
			bottom 20upx
			border-radius 20upx
			display flex
			align-items center
			justify-content space-around
			.box{
				height 160upx
				width 220upx
				background #f3f3f3;
				border-radius 20upx
				Flex()
				image{
					width 100upx
					height 100upx
				}
				.name{
					Font(32upx,#1296db,60upx,500)
				}
			}
		}
		.service-list{
			background #ffffff;
			border-radius 20upx
			.service{
				width 688upx
				height 100upx
				display flex
				align-items center
				position relative
				image{
					height 64upx
					width 64upx
					margin-left 20upx
				}
				.name{
					Font(32upx,#686868,64upx,500)
					margin-left 20upx
				}
				.arrows{
					position absolute
					right 28upx
					color #C0C0C0;
				}
				.line{
					width 620upx
					height 1upx
					background #C0C0C0;
					position absolute
					bottom 0upx
					left 34upx
				}
			}
		}
	}
</style>
