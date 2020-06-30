<script>
	export default {
		// 登录信息
		globalData: {
			isLogin:false,
			account:'',
			nickname:"未登录"
		},
		onLaunch: function() {
			console.log('App Launch')
			if(!getApp().globalData.isLogin)
			{
				uni.navigateTo({
					url:"pages/my/login/login"
				})
			}
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
</style>
