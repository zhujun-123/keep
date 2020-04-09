<template>
	<view class="loadmore">
		{{loadtext}}
	</view>
</template>

<script>
	export default {
		props:{
			loadtext: String
		}
	}
</script>

<style scoped>
	.loadmore {
		text-align: center;
		color: #AAAAAA;
		padding: 15upx;
	}
</style>
