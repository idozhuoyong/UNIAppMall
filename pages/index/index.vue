<template>
	<view class="container">
		<!-- 搜索 -->
		<uni-search-bar @confirm="search" @input="input" ></uni-search-bar>
		<!-- 公告 -->
		<view class="notice">
			<image class="notice-icon" src="../../static/images/commons/notice.png" mode=""></image>
			<swiper class="notice-swiper" :vertical="true" :autoplay="true" :interval="3000" :duration="1000" :circular="true">
				<swiper-item>
					<view class="swiper-item ellipsis">哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item ellipsis">222</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item ellipsis">333</view>
				</swiper-item>
			</swiper>
		</view>
		<!-- 菜单 -->
		<!-- 广告 -->
		<!-- 推荐产品 -->
		<!-- 砍价产品 -->
		<!-- 产品列表 -->
	</view>
</template>

<script>
	const WEBAPI = require('apifm-webapi')
	WEBAPI.init('idozhuoyong')
	
	import { uniSearchBar } from '@dcloudio/uni-ui'
	
	export default {
		components: { uniSearchBar },
		data() {
			return {
			}
		},
		onLoad() {
		},
		methods: {
			search(e) {
				console.log("===search===");
				console.log(e);
			},
			input(e) {
				console.log("===input===");
				console.log(e);
			}
		}
	}
</script>

<style>
	.ellipsis {
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}
	.notice {
		display: flex;
		flex-direction: row;
		height: 80rpx;
		align-items: center;
	}
	.notice-icon {
		width: 30rpx; 
		height: 30rpx;
		margin-left: 20rpx;
	}
	.notice-swiper {
		flex: 1;
		margin-left: 20rpx;
		margin-right: 20rpx;
		height: 100%;
	}
	.notice-swiper swiper-item {
		display: flex;
		align-items: center;
	}
</style>
