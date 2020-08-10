<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
		<tuozuai :dragDrop="dragDrop"/>
	</view>
</template>

<script>
	import tuozuai from '@/components/tuozuai/tz.vue' 

	export default {
		components:{tuozuai},
		data() { 
			return {
				title: 'Hello',
				dragDrop:{
					windowWidth:'',//屏幕宽度
					windowHeight:'' ,//屏幕高度
				}
			}
		},
		onLoad() {
			var self=this
			uni.getSystemInfo({
			    success: function (res) {
					
					self.dragDrop.windowWidth=res.windowWidth
					self.dragDrop.windowHeight=res.windowHeight
			    }
			});
		},
		methods: {

		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
