<template>
	<view>
		<swiper-tab-head :tabBars="tabBars" :tabIndex="tabIndex" @tabtap="tabtap" scrollItemStyle="width:33%;" />
		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{height:swiperheight+'px'}" :current="tabIndex" @change="tabChange">
				<swiper-item v-for="(items,index) in newslist" :key="index">
					<scroll-view scroll-y class="list" @scrolltolower="loadmore(index)" :show-scrollbar="false">
						<template v-if="items.list.length > 0">
							<!-- 图文列表 -->
							<block v-for="(item,index1) in items.list" :key="index1">
								<home-list :item="item" :index="index1" />
							</block>
							<!-- 上拉加载 -->
							<load-more :loadtext="items.loadtext" />
						</template>
						<template v-else>
							<!-- 无内容默认 -->
							<no-thing />
						</template>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import SwiperTabHead from "@/components/content/home/swiper-tab-head.vue"
	import HomeList from "@/components/content/home/home-list.vue";

	import LoadMore from "@/components/common/loadmore/load-more.vue";
	import NoThing from "@/components/common/nothing/no-thing.vue";

	export default {
		components: {
			SwiperTabHead,
			HomeList,
			LoadMore,
			NoThing
		},
		data() {
			return {
				tabIndex: 0,
				swiperheight: 500,
				tabBars: [{
						name: "关注",
						id: "guanzhu"
					},
					{
						name: "推荐",
						id: "tuijian"
					},
					{
						name: "热门",
						id: "remen"
					}
				],
				newslist: [{
						loadtext: "上拉加载更多",
						list: [{
								userpic: "../../static/sport/1.jpg",
								username: "昵称",
								isguanzhu: false,
								title: "我是标题",
								type: "img", // img:图文,video:视频
								titlepic: "../../static/sport/2.jpeg",
								infonum: {
									index: 0, //0:没有操作，1:顶,2:踩；
									dingnum: 11,
									cainum: 11,
								},
								commentnum: 10,
								sharenum: 10,
							},
							{
								userpic: "../../static/sport/1.jpg",
								username: "昵称",
								isguanzhu: true,
								title: "我是标题",
								type: "video", // img:图文,video:视频
								titlepic: "../../static/sport/10.jpg",
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
					},
					{
						loadtext: "上拉加载更多",
						list: [{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "昵称",
								isguanzhu: false,
								title: "我是标题",
								type: "img", // img:图文,video:视频
								titlepic: "../../static/sport/3.jpeg",
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
					},
					{
						loadtext: "上拉加载更多",
						list: []
					}
				]
			};
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res) => {
					let height = res.windowHeight - uni.upx2px(100)
					this.swiperheight = height;
				}
			});
		},
		//监听搜索框点击事件
		onNavigationBarSearchInputClicked() {
			uni.navigateTo({
				url: '../search/search'
			})
		},
		//监听原生标题导航按钮
		onNavigationBarButtonTap(e) {
			switch (e.index) {
				case 1:
					//打开发布页面
					uni.navigateTo({
						url: './add-input/add-input'
					})
					break;
			}
		},
		methods: {
			//上拉加载
			loadmore(index) {
				if (this.newslist[index].loadtext != "上拉加载更多") {
					return;
				}
				this.newslist[index].loadtext = "加载中..."
				setTimeout(() => {
					let obj = {
						userpic: "../../static/demo/userpic/12.jpg",
						username: "昵称",
						isguanzhu: false,
						title: "我是标题",
						type: "img", // img:图文,video:视频
						titlepic: "../../static/sport/5.jpeg",
						infonum: {
							index: 0, //0:没有操作，1:顶,2:踩；
							dingnum: 11,
							cainum: 11,
						},
						commentnum: 10,
						sharenum: 10,
					}
					this.newslist[index].list.push(obj)
					this.newslist[index].loadtext = "上拉加载更多"
				}, 500)

				//this.newslist[index].loadtext="没有更多数据了"
			},
			//tabbar点击事件
			tabtap(index) {
				this.tabIndex = index
			},
			//滑动事件
			tabChange(e) {
				this.tabIndex = e.detail.current;
			}
		}
	}
</script>

<style lang="scss">

</style>
