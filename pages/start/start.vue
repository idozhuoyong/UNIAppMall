<template>
	<view class="container">
		<swiper class="swiper" :indicator-dots="banners.length > 1" active-class="swiper" @change="swiperChange">
			<swiper-item v-for="item in banners" :key="item.id">
				<image class="swiper" :src="item.picUrl" mode=""></image>
			</swiper-item>
		</swiper>
		<view class="btn-container" v-if="currentIndex == banners.length-1">
			<button size="mini" type="primary" @tap="onHandlerGoToMall">进入店铺</button>
		</view>
	</view>
</template>

<script>
	const WEBAPI = require('apifm-webapi')
	WEBAPI.init('idozhuoyong')
	let _this;
	
	export default {
		data() {
			return {
				currentIndex: 0,
				banners: []
			}
		},
		/**
		 * 监听页面加载
		 */
		onLoad() {
			_this = this;
			/**
			 * WXAPI 方法返回数据主要包含 3 个内容：
			 * 1. code 错误码，0 代表操作重构，其他数字均表示错误，具体错误描述请查看 msg；
			 * 2. msg 如果上面的code不为0，那么 msg 将会返回具体的错误说明描述
			 * 3. data 字段保存了 code 为0 时候的数据，一起你需要的数据，都保存在 data 中返回给你
			 */
			uni.getStorage({
				key: "firstLaunchApplicationFlag",
				success(res) {
					if (res.data == "1" && _this.banners.length == 0) {
						// 不是第一次进入应用，直接进入店铺
						_this.onHandlerGoToMall();
					}
				}
			})
			uni.showLoading({
				title: '加载中...',
				mask: false
			});
			// 网络加载广告数据
			WEBAPI.banners({type: "app"}).then(res => {
				console.log(res);
				if (res.code === 0 && res.data.length > 0) {
					this.banners = res.data;
				} else {
					// 请求失败，直接进入店铺
					this.onHandlerGoToMall();
				}
			}).catch(err => {
				// 请求失败，直接进入店铺
				this.onHandlerGoToMall();
			}).finally(() => {
				uni.hideLoading();
			});
		},
		methods: {
			/**
			 * banner图切换
			 */
			swiperChange(e) {
				this.currentIndex = e.detail.current;
			},
			/**
			 * 进入店铺
			 */
			onHandlerGoToMall() {
				uni.setStorage({
					key: "firstLaunchApplicationFlag",
					data: "1"
				});
				uni.switchTab({
					url: "../index/index"
				})
			}
		}
	}
</script>

<style scoped>
	.swiper {
		width: 100vw;
		height: 100vh;
	}
	.btn-container {
		position: fixed;
		bottom: 60rpx;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		width: 100%;
	}
</style>
