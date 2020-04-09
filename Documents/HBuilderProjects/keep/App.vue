<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
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
	@import './common/css/uni.css';
	/* 公共样式 */
	@import './common/css/common.css';
	/* 引入自定义图标库 */
	@import './common/css/icon.css';
	/* 引入css动画库 */
	@import './common/css/animate.css';
</style>
