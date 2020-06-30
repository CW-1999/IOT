<!-- 首页 06271555 BY CW -->
<!-- 修改者 	修改时间 	修改内容 -->
<template>
	<view class="home">
		<!-- 导航栏 start -->
			<view class="title">所有房间</view>
		<!-- 导航栏 end -->
		<!-- 房间列表 start -->
			<view class="list">
				<!-- 单个房间 start -->
					<view class="box" v-for="(item,index) in list" :key="index" @click="To(item.path)">
						<!-- 房间icon start -->
							<image :src="item.iconpath"></image>
						<!-- 房间icon end -->
						<!-- 房间名称 start -->
							<view class="name">
								{{item.name}}
							</view>
						<!-- 房间名称 end -->
					</view>
				<!-- 单个房间 end -->
			</view>
		<!-- 房间列表 end -->
	</view>
</template>

<script>
export default {
	data() {
		return {
			list:[
				{
					iconpath:"/static/home-icon/ic-bedroom.png",
					path:"/pages/home/room/room",
					name:"主卧"
				},
				{
					iconpath:"/static/home-icon/ic-kidsroom.png",
					path:"/pages/home/room/room",
					name:"侧卧"
				},
				{
					iconpath:"/static/home-icon/ic-drawing-room.png",
					path:"",
					name:"客厅"
				},
				{
					iconpath:"/static/home-icon/ic-balcony.png",
					path:"",
					name:"阳台"
				},
				{
					iconpath:"/static/home-icon/ic-kitchen.png",
					path:"",
					name:"厨房"
				},
				{
					iconpath:"/static/home-icon/ic-dening-room.png",
					path:"",
					name:"餐厅"
				},
				{
					iconpath:"/static/home-icon/ic-toilet.png",
					path:"",
					name:"卫生间"
				},
			]
		}
	},
	onLoad() {
		console.log("home show")
	},
	methods: {
		To(Url){
			console.log(Url)
			uni.navigateTo({
				url:Url
			})
		}
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
	.home{
		width 750upx
		background #F6F7FB;
		Flex()
		.title{
			height 80upx
			width 688upx
			Font(40upx,#000000,80upx,bold,left)
		}
		.list{
			width 688upx
			display flex
			flex-wrap wrap
			justify-content space-between
			.box{
				margin-bottom 20upx
				width 334upx
				height 334upx
				background #FFFFFF;
				border-radius 20upx
				Flex()
				image{
					width 128upx
					height 128upx
					margin-top 60upx
					border-radius 20upx
				}
				.name{
					margin-top 20upx
					Font(32upx,#000000,32upx,bold)
				}
			}
		}
	}
</style>

