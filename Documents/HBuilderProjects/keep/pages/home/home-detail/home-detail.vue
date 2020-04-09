<template>
	<view>
		<detail-info :item="detail" />

		<!-- 评论区 -->
		<view class="u-comment-title">最新评论{{comment.count}}</view>
		<view class="uni-comment u-comment">
			<block v-for="(item, index) in comment.list" :key="index">
				<comment-list :item="item" :index="index" />
			</block>
		</view>
		
		<view style="height: 120upx;" />
		
		<!-- 输入框 -->
		<user-chat-bottom @submit="submit" />
		<!-- 分享 -->
		<more-share :show="shareshow" @togle="togle"/>
	</view>
</template>

<script>
	import detailInfo from "@/components/content/home-detail/detail-info.vue"
	import commentList from "@/components/content/home-detail/comment-list.vue"
	import userChatBottom from "@/components/common/user-chat/user-chat-bottom.vue"
	import moreShare from "@/components/common/more-share.vue"
	
	import time from "@/common/utils/time.js"

	export default {
		components: {
			detailInfo,
			commentList,
			userChatBottom,
			moreShare
		},
		data() {
			return {
				shareshow: false,
				comment: {
					count: 20,
					list: []
				},
				detail:
				//图文
				{
					userpic: "../../../static/demo/userpic/12.jpg",
					username: "昵称",
					sex: 0, //0 男  1 女
					age: 25,
					isguanzhu: false,
					title: "我是阿萨德离开家哈三联快点安康老师当老师的卢卡斯拉屎德令哈市来看待哈拉斯柯达多斯拉克和当老师拉上客户的凉开水德里克哈三李的喀什廖凯标题",
					titlepic: "../../../static/demo/datapic/13.jpg",
					morepic: [ "../../../static/sport/2.jpeg"],
					video: false,
					share: false,
					path: "深圳 龙岗",
					sharenum: 20,
					commentnum: 30,
					goodnum: 40
				}
			}
		},
		onLoad(e) {
			this.initdata(JSON.parse(e.detailData))
			this.getcomment()
			//设置导航标题
			uni.setNavigationBarTitle({
			            title: "动态详情"
			        });
		},
		//监听导航右边按钮点击
		onNavigationBarButtonTap(e) {
			if (e.index == 0) {
				this.togle()
			}
		},
		methods: {
			togle() {
				this.shareshow = !this.shareshow
			},
			//获取评论
			getcomment() {
				let arr = [
					//一级评论
					{
						id: 1,
						fid: 0,
						userpic: "../../../static/demo/userpic/13.jpg",
						username: "昵称",
						time: "1583506349",
						data: "支持国产，支持DCloud!"
					},
					//子级评论
					{
						id: 2,
						fid: 1,
						userpic: "../../../static/demo/userpic/13.jpg",
						username: "昵称",
						time: "1583506349",
						data: "支持国产，支持DCloud!"
					},
					{
						id: 3,
						fid: 1,
						userpic: "../../../static/demo/userpic/13.jpg",
						username: "昵称",
						time: "1583506349",
						data: "支持国产，支持DCloud!"
					},
					{
						id: 4,
						fid: 0,
						userpic: "../../../static/demo/userpic/13.jpg",
						username: "昵称",
						time: "1583506349",
						data: "支持国产，支持DCloud!"
					}
				]
				for (var i = 0; i < arr.length; i++) {
					arr[i].time = time.gettime.gettime(arr[i].time)
				}
				this.comment.list = arr
			},
			//初始化数据
			initdata(obj) {
				//修改窗口
				uni.setNavigationBarTitle({
					title: obj.title
				})
			},
			submit(data) {
				//构建数据
				let now = new Date().getTime()
				let obj = {
						id: 1,
						fid: 0,
						userpic: "../../static/demo/userpic/13.jpg",
						username: "小猫咪",
						time: time.gettime.gettime(new Date().getTime()),
						data: data
					}
				this.comment.list.push(obj)
			}
		}
	}
</script>

<style>
	/* 分享区 */
	
	/* 评论区 */
	.u-comment-title {
		padding: 20upx;
		font-size: 30upx;
		font-weight: bold;
	}

	.u-comment {
		padding: 0 20upx;
	}
</style>
