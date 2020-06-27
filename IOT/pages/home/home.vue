<!-- 首页 06271555 BY CW -->
<!-- 修改者 	修改时间 	修改内容 -->
<template>
	<view>
		<button type="primary" @click="connect">mqtt 连接</button>
		<button type="primary" @click="subscribe">mqtt 订阅</button>
		<button type="primary" @click="publish">mqtt 发布</button>
		<button type="primary" @click="unsubscribe">取消订阅</button>
		<button type="primary" @click="unconnect">断开连接</button>
		<view>message:{{ message }}</view>
	</view>
</template>

<script>
import mqtt from '../../utils/mqtt.js';
export default {
	data() {
		return {
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
				clientId: 'H5-1740707273',
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
	methods: {
		// 消息刷新
		change(e) {
			console.log(e.show);
		},
		// 连接服务器
		connect(){
			this.client = mqtt.connect(
				this.host,
				this.options
			);
			this.client.on('connect', () => {
				console.log('连接成功');
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
				this.message = message.toString();
			});
		},
		// 订阅消息
		subscribe(){
			// 判断是否已成功连接
			if (!this.client.connected) {
				console.log('客户端未连接');
				return;
			}

			this.client.subscribe('one', { qos: 1 }, error => {
					if (!error) {
						console.log('订阅成功');
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
		publish() {
			// 判断是否已成功连接
			if (!this.client.connected) {
				console.log('客户端未连接');
				return;
			}
			// publich(topic, payload, options/callback)
			this.client.publish('one', this.time.toString(), error => {
				console.log(error || '消息发布成功');
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
};
</script>
<style>
button {
	margin-top: 30upx;
	margin-bottom: 30upx;
}
</style>

