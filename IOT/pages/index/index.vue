<!-- 门禁页面 06271540 BY CW -->
<!-- 修改者 	修改时间 	修改内容 -->
<template>
	<view class="index">
		<!-- 自定义导航栏 Start -->
			<view class="navigation">
				<!-- 返回按钮 -->
					<view class="back">
						<image src="/static/entranceGuard-icon/ic-back.png" mode="aspectFit" style="width: 48upx;height: 48upx;"></image>
					</view>
				<!-- 返回按钮 -->
				<!-- 门锁图标 Start-->
					<view class="doorLock">
						<image src="/static/entranceGuard-icon/ic-doorLock.png" mode="aspectFit" style="width: 192upx;height: 192upx;"></image>
					</view>
				<!-- 门锁图标 end-->
			</view>
		<!-- 自定义导航栏 end -->
		<!-- 滑动开锁 Start -->
			<movable-area class="unlocking">
				<!-- 滚动条背景颜色 Start -->
					<view class="text">
						滑动解锁
					</view>
				<!-- 滚动条背景颜色 end -->
				<!-- 滑动按钮 Start-->
					<movable-view @change="onChange" inertia="true" direction="horizontal" :x="x" :y="y">
						>
					</movable-view>
				<!-- 滑动按钮 end-->
			</movable-area>
		<!-- 滑动开锁 Start -->
		<!-- 密码管理 门卡管理 用户权限 Start -->
			<view class="service">
				<!-- 单项服务box Start -->
					<view class="box" v-for="(item,index) in service" :key="index">
						<!-- 服务图标 Start-->
							<view class="icon">
								<image :src="item.iconpath" mode="aspectFit" style="width: 100upx;height: 100upx;"></image>
							</view>
						<!-- 服务图标 end-->
						<!-- 服务名称 Start-->
							<view class="text">
								{{item.name}}
							</view>
						<!-- 服务名称 end-->
					</view>
				<!-- 单项服务box end -->
			</view>
		<!-- 密码管理 门卡管理 用户权限 end-->
		<!-- 开锁日志 Start -->
			<view class="log">
				<!-- 上半部分 Start-->
					<view class="top">
						<!-- 标题 Start -->
							<view class="title">
								今日门锁日志
							</view>
						<!-- 标题 end -->
						<!-- 历史数据 Start-->
							<view class="history">
								历史数据>
							</view>
						<!-- 历史数据 end-->
					</view>
				<!-- 上半部分 end-->
				<scroll-view scroll-y="true">
					<!-- 记录 Start -->
						<view class="list" v-for="(item,index) in list" :key="index">
							<!-- 头像 Start -->
								<view class="headPortrait">
									
								</view>
							<!-- 头像 end -->
							<!-- 姓名 Start-->
								<view class="name">
									{{item.name}}
								</view>
							<!-- 姓名 end-->
							<!-- 时间 Start-->
								<view class="time">
									{{item.time}}
								</view>
							<!-- 时间 end -->
							<!-- 开门方式 Start -->
								<view class="way">
									{{item.way}}
								</view>
							<!-- 开门方式 end -->
						</view>
					<!-- 记录 end -->
				</scroll-view>
			</view>
		<!-- 开锁日志 end -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				x:0,
				y:0,
				service:[
					{
						iconpath:"/static/entranceGuard-icon/ic-password.png",
						name:"密码管理"
					},
					{
						iconpath:"/static/entranceGuard-icon/ic-doorCard.png",
						name:"门卡管理"
					},
					{
						iconpath:"/static/entranceGuard-icon/ic-userPermissions.png",
						name:"用户权限"
					}
				],
				list:[
					{
						iconpath:"",
						name:"刘鉴延",
						time:"2020-06-16 21:41",
						way:"鸡巴开门"
					},
					{
						iconpath:"",
						name:"P哥",
						time:"2020-06-16 21:41",
						way:"屁股开门"
					},
					{
						iconpath:"",
						name:"刘老师",
						time:"2020-06-16 21:41",
						way:"牙齿开门"
					},
					{
						iconpath:"",
						name:"刘鉴延",
						time:"2020-06-16 21:41",
						way:"阿姨开门"
					},
				]
			}
		},
		onLoad() {

		},
		methods: {
			onChange(event){
				if(event.detail.x>260)
				{
					console.log("解锁")
				}
			}
		}
	}
</script>

<style lang="stylus">
	Display(){
		display flex
		flex-direction column
		align-items center
	}
	.index{
		height calc(100vh - 94upx)
		/* #ifdef MP */
		height 100vh
		/* #endif */
		width 750upx
		background #dcdcdc;
		Display()
		.navigation{
			height 500upx
			width 750upx
			Display()
			background linear-gradient(67deg,rgba(30, 115, 242, 1.0) 33%,rgba(95, 244, 251, 1.0) 100%)
			.back{
				height 48upx
				width 48upx
				border-radius 50%
				position absolute
				z-index 100
				top 60upx
				left 32upx
			}
			.doorLock{
				margin-top 150upx
			}
		}
		.unlocking{
			width 668upx
			height 128upx
			background #FFFFFF
			position absolute
			top 432upx
			border-radius 64upx
			border 1upx solid #007AFF
			z-index 9
			text-align center
			line-height 128upx
			font-weight bold
			letter-spacing 1em
			text-indent 1em
			.text{
				background: linear-gradient(to right, blue, white);
				-webkit-background-clip: text;
				color: transparent;
			}
			movable-view{
				height 116upx
				width 116upx
				position absolute
				top 6upx
				left 6upx
				border-radius 50%
				background #007AFF
				font-size 80upx
				text-align center
				line-height 100upx
				color #FFFFFF;
			}
		}
		.service{
			width 750upx
			height 300upx
			background #FFFFFF
			display flex
			align-items center
			.box{
				height 300upx
				width 250upx
				Display()
				color #333333
				.icon{
					margin-top 84upx
					width 100upx
					height 100upx
				}
				.text{
					margin-top 20upx
					color #007AFF
					font-size 32upx
					width 250upx
					text-align center
					height 32upx
					line-height 32upx
				}	
			}	
		}	
		.log{
			margin-top 16upx
			width 750upx
			height calc(100vh - 907upx)
			/* #ifdef MP */
			height calc(100vh - 813upx)
			/* #endif */
			background #FFFFFF
			border-radius 20upx
			.top{
				display flex
				justify-content space-between
				.title{
					width 240upx
					height 64upx
					line-height 64upx
					font-size 32upx
					text-align center
					font-weight bold
				}
				.history{
					text-align center
					width 160upx
					height 64upx
					line-height 64upx
					font-size 24upx
				}
			}
			scroll-view{
				height calc(100vh - 971upx)
				/* #ifdef MP */
				height calc(100vh - 877upx)
				/* #endif */
				.list{
					height 128upx
					border-bottom 1upx solid #007AFF
					position relative
					.headPortrait{
						width 100upx
						height 100upx
						border-radius 50%
						background #1ba5fb;
						position absolute
						top 14upx
						left 32upx
					}
					
					.name{
						font-size 32upx
						width 400upx
						position absolute
						top 16upx
						left 164upx
						font-weight 600
					}
					
					.time{
						font-size 24upx
						width 400upx
						position absolute
						left 164upx
						top 64upx
					}
					.way{
						font-size 28upx
						position absolute
						width 160upx
						text-align center
						right 32upx
						top  42upx
						background linear-gradient(67deg,rgba(30, 115, 242, 1.0) 33%,rgba(95, 244, 251, 1.0) 100%)
						border-radius 20upx
						font-weight bold
					}	
				}	
			}
		}
	}
	
</style>
