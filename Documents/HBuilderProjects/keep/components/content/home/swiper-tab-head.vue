<template>
		<view class="uni-tab-bar">
			<scroll-view scroll-x class="uni-swiper-tab" :style="scrollStyle">
				<block v-for="(tab,index) in tabBars" :key="tab.id">
					<view class="swiper-tab-list" 
					:class="{'active':tabIndex==index}"
					@tap="tabtap(index)"
					:style="scrollItemStyle">
						{{tab.name}} {{tab.num?tab.num:''}}
						<view class="swiper-tab-line"/>
					</view>
				</block>
			</scroll-view>
		</view>
</template>

<script>
	export default {
		props: {
			tabBars: Array,
			tabIndex: Number,
			scrollStyle: {
				type: String,
				default: ""
			},
			scrollItemStyle: {
				type: String,
				default: ""
			}
		},
		methods: {
			tabtap(index) {
				this.$emit('tabtap',index)
			}
		}
	}
</script>

<style scoped>
	.uni-swiper-tab{
		border-bottom: 1upx solid #EEEEEE;
	}
	.swiper-tab-list {
		color: #969696;
		font-weight: bold;
	}
	.uni-tab-bar .active{
		color: #343434;
	}
	.active .swiper-tab-line {
		border-bottom: 2upx solid #515151;
		width: 38upx;
		margin: auto;
		border-top: 2upx solid #515151;
		border-radius: 20upx;
	}
</style>
