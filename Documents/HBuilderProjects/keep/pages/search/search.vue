<template>
	<view class="">
		<!-- 图文列表 -->
		<template v-if="list.length > 0">
		<block v-for="(item,index) in list" :key="index">
			<home-list :item="item" :index="index" />
		</block>
		<!-- 上拉加载 -->
		<load-more :loadtext="loadtext" />
		</template>
		
		<template v-else-if="issearch && list.length < 1">
			<!-- 无内容默认 -->
			<no-thing />
		</template>
	</view>
</template>

<script>
	import HomeList from "../../components/content/home/home-list.vue";
	import NoThing from "../../components/common/nothing/no-thing.vue";
	import LoadMore from "../../components/common/loadmore/load-more.vue";
	
	export default {
		components: {
			HomeList,
			NoThing,
			LoadMore
		},
		data() {
			return {
				issearch: false,
				loadtext: "上拉加载更多",
				list: [],
				searchtext: ""
			}
		},
		//监听原生标题导航按钮事件(取消按钮)
		onNavigationBarButtonTap(e) {
			if(e.index == 0) {
				uni.navigateBack({
						delta: 1
				})
			}
		},
		//监听搜索框文本变化
		onNavigationBarSearchInputChanged(e) {
			this.searchtext = e.text
		},
		//监听点击搜索按钮事件
		onNavigationBarSearchInputConfirmed(e) {
			if(e.text) {
				this.getdata()
			}
		},
		//监听触底事件
		onReachBottom() {
			this.loadmore()
		},
		//监听下拉刷新
		onPullDownRefresh() {
			this.getdata()
			//关闭下拉刷新
			uni.stopPullDownRefresh();
		},
		methods: {
			//搜索事件
			getdata() {
				//请求服务器  post keyword: this.searchtext
				uni.showLoading({});
				setTimeout(() => {
					let arr = [
						{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							isguanzhu: false,
							title: "我是标题",
							type: "img", // img:图文,video:视频
							titlepic: "../../static/demo/datapic/11.jpg",
							infonum: {
								index: 0, //0:没有操作，1:顶,2:踩；
								dingnum: 11,
								cainum: 11,
							},
							commentnum: 10,
							sharenum: 10,
						},
						{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							isguanzhu: true,
							title: "我是标题",
							type: "video", // img:图文,video:视频
							titlepic: "../../static/demo/datapic/11.jpg",
							playnum: "20w",
							long: "2:47",
							infonum: {
								index: 1, //0:没有操作，1:顶,2:踩；
								dingnum: 11,
								cainum: 11,
							},
							commentnum: 10,
							sharenum: 10,
						}
					]
					this.list = arr
					uni.hideLoading()
					this.issearch = true
				},500)
			},
			//上拉加载
			loadmore() {
				if (this.list.loadtext != "上拉加载更多") {
					return;
				}
				this.list.loadtext = "加载中..."
				setTimeout(() => {
					let obj = {
						userpic: "../../static/demo/userpic/12.jpg",
						username: "昵称",
						isguanzhu: false,
						title: "我是标题",
						type: "img", // img:图文,video:视频
						titlepic: "../../static/demo/datapic/11.jpg",
						infonum: {
							index: 0, //0:没有操作，1:顶,2:踩；
							dingnum: 11,
							cainum: 11,
						},
						commentnum: 10,
						sharenum: 10,
					}
					this.list.list.push(obj)
					this.list.loadtext = "上拉加载更多"
				}, 500)
				//this.list.loadtext="没有更多数据了"
			},
		},
	}
</script>

<style>
</style>
