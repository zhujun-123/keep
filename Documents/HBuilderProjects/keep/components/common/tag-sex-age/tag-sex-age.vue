<template>
	<view class="tag-sex icon iconfont" 
	:class="[sex==0?'icon-nan':'icon-nv']">
		{{age}}
	</view>
</template>

<script>
	export default {
		props: {
			sex: Number,
			age: Number
		}
	}
</script>

<style scoped>
	.tag-sex {
		background: #007AFF;
		color: #FFFFFF;
		font-size: 23upx;
		padding: 2upx 10upx;
		margin-left: 15upx;
		border-radius: 20upx;
		line-height: 21upx;
	}
	
	.icon-nv {
		background: #FF698D!important;
	}
</style>
