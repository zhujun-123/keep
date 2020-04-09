<template>
	<view class="common-list u-f animated fadeInLeft fast">
		<view class="common-list-l">
			<image :src="item.userpic" mode="widthFix" lazy-load />
		</view>
		<view class="common-list-r">
			<view>
				<view class="u-f-ac u-f-jsb">
					<view class="u-f-ac">
						{{item.username}}
						<tag-sex-age :sex="item.sex" :age="item.age" />
					</view>
					<view v-show="!isguanzhu" class="icon iconfont icon-zengjia" @tap="guanzhu">
						关注
					</view>
				</view>
				<view class="common-list-r-time"> 26天前 </view>
			</view>

			<view class="content">{{item.title}}</view>
			<view class="content">
				<!-- 图片 -->
				<view class="only-img" v-if="item.morepic.length === 1">
					<image :src="item.morepic[0]" mode="scaleToFill" lazy-load  @tap="imgdetail(index)" />
				</view>
				<block v-else v-for="(img, index) in item.morepic" :key="index" class="img">
					<image :src="img" mode="widthFix" lazy-load @tap="imgdetail(index)" />
				</block>
				<!-- 视频 -->
				<template v-if="item.video">
					<view class="common-list-play icon iconfont icon-bofang" />
					<view class="common-list-playinfo">
						{{item.video.looknum}} 次播放 {{item.video.long}}
					</view>
				</template>
				<!-- 分享 -->
				<view v-if="item.share" class="common-list-share u-f-ac">
					<image :src="item.titlepic" mode="widthFix" lazy-load />
					<view>
						{{item.share.title}}
					</view>
				</view>

			</view>
			<view class="u-f-ac u-f-jsb content">
				<view>{{item.path}}</view>
				<view class="u-f-ac">
					<view class="icon iconfont icon-zhuanfa">
						{{item.sharenum}}
					</view>
					<view class="icon iconfont icon-pinglun1">
						{{item.commentnum}}
					</view>
					<view class="icon iconfont icon-dianzan1">
						{{item.goodnum}}
					</view>
				</view>
			</view>
		</view>
	</view>

</template>

<script>
	import tagSexAge from "../../common/tag-sex-age/tag-sex-age.vue"

	export default {
		components: {
			tagSexAge
		},
		props: {
			item: Object
		},
		data() {
			return {
				isguanzhu: this.item.isguanzhu
			}
		},
		methods: {
			guanzhu() {
				this.isguanzhu = true
				uni.showToast({
					title: '关注成功'
				})
			},
			imgdetail(index) {
				uni.previewImage({
					current: index,
					urls: this.item.morepic
				})
			}
		}
	}
</script>

<style scoped>
	@import "../../../common/css/list.css";

	.common-list-r {
		border-bottom: 0;
	}

	.common-list {
		border-bottom: 1upx solid #EEEEEE;
	}

	.common-list-r-time {
		padding: 15upx 0;
		color: #CCCCCC !important;
		font-size: 25upx;
		background: #FFFFFF !important;
	}

	.common-list-r>view:nth-child(1)>view:nth-child(1)>view:first-child {
		color: #999999;
		font-size: 33upx;
	}

	.common-list-r>view:nth-child(1)>view:nth-child(1)>view:last-child {
		background: #EEEEEE;
		padding: 0 10upx;
		font-size: 26upx;
	}
</style>
