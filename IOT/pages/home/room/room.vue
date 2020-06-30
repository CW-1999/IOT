<!-- 房间 06282217 BY CW -->
<!-- 修改者 	修改时间 	修改内容 -->
<template>
	<view class="room" :style="bg">
		<!-- 灯泡 start -->
			<image v-if="isLight=='1'" class="light" src="/static/home-icon/room-icon/ic-light-open.png" @click="lightUp()"></image>
			<image v-if="isLight!='1'" class="light" src="/static/home-icon/room-icon/ic-light.png" @click="lightUp()"></image>
		<!-- 灯泡 end -->
		
		<!-- 空调 start -->
			<image v-if="isCooling=='1'" class="cooling" src="/static/home-icon/room-icon/ic-air-conditioner-open.png" @click="cooling()"></image>
			<image v-if="isCooling!='1'" class="cooling" src="/static/home-icon/room-icon/ic-air-conditioner.png" @click="cooling()"></image>
		<!-- 空调 end -->
		
		<!-- 温湿度 start -->
			<view class="humiture">
				<!-- 体感温度 start -->
					<view class="temperature-text">
						体感温度
					</view>
				<!-- 体感温度 end -->
				<!-- 温度 start -->
					<view class="temperature">
						{{wd}}°
					</view>
				<!-- 温度 end -->
				<!-- 相对湿度 start -->
					<view class="humidity">
						相对湿度：
						<text>{{sd}}%</text>
					</view>
				<!-- 相对湿度 end -->
			</view>
		<!-- 温湿度 end -->
		
		<!-- 当前状态 start -->
			<view class="state">
				当前状态：
				<text v-if="isConnect" style="color: #25f14d;">在线</text>
				<text v-else style="color: #ff3300;">离线</text>
			</view>
		<!-- 当前状态 end -->
		
		<!-- 连接 start -->
			<view class="connect" @click="btn()">
				连接
			</view>
		<!-- 连接 end -->
	</view>
</template>

<script>
import mqtt from '../../../utils/mqtt.js';
export default {
	data() {
		return {
			// 连接状态
			isConnect:false,
			// 背景颜色
			bg:'background:linear-gradient(0deg,rgba(30, 115, 242, 1.0) 33%,rgba(95, 244, 251, 1.0) 100%);',
			// 灯光开关状态
			isLight:false,
			// 空调开关状态
			isCooling:false,
			// 温度
			wd:26,
			// 湿度
			sd:80,
			// #ifdef H5
			host: 'ws://121.37.199.83:8083/mqtt',
			//#endif
			// #ifdef MP-WEIXIN || APP-PLUS
			host: 'wxs://121.37.199.83:8083/mqtt',
			//#endif
			client: null,
			//记录重连的次数
			reconnectCounts: 0,
			//MQTT连接的配置
			message: "",
			time: 1,
			options: {
				wsOptions: {},
				protocolVersion: 4, //MQTT连接协议版本
				clientId: '',
				clean: false,
				password: '',
				username: '',
				reconnectPeriod: 1000, //1000毫秒，两次重新连接之间的间隔
				connectTimeout: 30 * 1000, //1000毫秒，两次重新连接之间的间隔
				resubscribe: true //如果连接断开并重新连接，则会再次自动订阅已订阅的主题（默认true）
			},
			content: '',
			type: 'center',
			popup: 'popup'
		};
	},
	onLoad() {
		// 把mqtt连接号设为登录账号
		this.options.clientId=getApp().globalData.account
	},
	onUnload() {
		// 与mqtt服务器断开连接
		if(this.isConnect){
			this.unconnect()
		}
	},
	methods: {
		// 点击灯泡
		lightUp(){
			//为开灯状态下
			if(this.isLight=='1'){
				// 发送关灯指令
				this.publish('0')
				this.isLight=false
			}
			else{
				// 发送开灯指令
				this.publish('1')
				this.isLight=true
			}
		},
		// 点击空调
		cooling(){
			//为开启状态下
			if(this.isCooling){
				// 发送关机指令
				this.publish('2')
				this.isCooling=false
			}
			else{
				// 发送开机指令
				this.publish('3')
				this.isCooling=true
			}
		},
		// 消息刷新
		change(e) {
			console.log(e.show);
		},
		// 点击连接按钮
		btn(){
			if(!this.isConnect)
			{
				uni.showLoading({
					title:"正在连接"
				})
				this.connect()
			}
		},
		// 连接服务器
		connect(){
			this.client = mqtt.connect(
				this.host,
				this.options
			);
			this.client.on('connect', () => {
				console.log('连接成功');
				// 订阅消息，接收温湿度信息
				this.subscribe()
				uni.hideLoading()

			});
			this.client.on('reconnect', error => {
				console.log('正在重连:', error);
			});
			this.client.on('error', error => {
				console.log('连接失败:', error);
			});
			// 为 message 时间添加处理函数
			this.client.on('message', (topic, message) => {
				console.log('收到来自', topic, '的消息', message.toString());
				switch(topic){
					case 'phone': console.log("控制消息")
					switch(message.toString()){
						case '0':console.log("关灯");break;
						case '1':console.log("开灯");break;
						case '2':console.log("关空调");break;
						case '3':console.log("开空调");break;
					}
					;break;
					case this.options.clientId: console.log("温湿度消息")
					this.wd = message.toString().substring(0,2);
					this.sd = message.toString().substring(2,4);
					;break;
				}
			});
		},
		// 订阅消息
		subscribe(){
			// 判断是否已成功连接
			if (!this.client.connected) {
				console.log('客户端未连接');
				return;
			}

			this.client.subscribe(this.options.clientId, { qos: 1 }, error => {
					if (!error) {
						console.log('订阅成功');
						this.isConnect=true
						}
				});

			// 订阅多个主题
			// this.client.subscribe(['one', 'two', 'three'], { qos: 1 }, err => {
			// 	console.log(err || '订阅成功');
			// 	this.show(err || '订阅成功');
			// // });
			/*
				    // 订阅不同 qos 的不同主题
				    this.client.subscribe(
				        [
				            { hello: 1 },
				            { 'one/two/three': 2 },
				            { '#': 0 }
				        ],
				        (err) => {
				          this.show();console.log(err || '订阅成功')
				        },
				    )


			});*/
		},
		// 发布消息
		publish(instruct) {
			// 判断是否已成功连接
			if (!this.client.connected) {
				console.log('客户端未连接');
				return;
			}
			// publich(topic, payload, options/callback)
			this.client.publish('phone',instruct.toString(), error => {
				console.log(error || instruct);
				this.time++;
			});
		},
		// 取消订阅
		unsubscribe() {
			this.client.unsubscribe(
				// topic, topic Array, topic Array-Onject
				// ['one', 'two', 'three'],
				'one',
				err => {
					console.log(err || '取消订阅成功');
				}
			);
		},
		// 断开服务器连接
		unconnect() {
			this.client.end();
			console.log('断开连接');
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
	.room{
		width 750upx
		height calc(100vh - 88upx)
		Flex()
		.light{
			width 180upx
			height 180upx
			margin-top 60upx
		}
		.cooling{
			width 280upx
			height 180upx
			margin-top 60upx
		}
		.humiture{
			width 500upx
			height 500upx
			border 15upx double #FFFFFF;
			border-radius 50%
			margin-top 40upx
			Flex()
			justify-content center
			.temperature-text{
				Font(28upx,#ffffff,28upx,500)
				margin-bottom 20upx
			}
			.temperature{
				Font(200upx,#ffffff,200upx,bold)
			}
			.humidity{
				Font(24upx,#ffffff,24upx,500)
				margin-top 20upx
				text{
					Font(28upx,#ffffff,28upx,500)
				}
			}
		}
		.state{
			Font(32upx,#FFFFFF,32upx,500)
			margin-top 40upx	
		}
		.connect{
			Font(32upx,#FFFFFF,64upx,500)
			margin-top 30upx
			letter-spacing 24upx
			text-indent 24upx
			background #52ff34;
			border-radius 32upx
			width 160upx
		}
	}
</style>
