<template>
	<view class="about">
		<view class="content">
			<image class="logo" src="/static/logo.png"></image>
			<view class="text-area">
				<text class="title">{{title}}</text>
			</view>


			<button type="primary" @click="testAsyncFunc">获取oaid</button>

			<button type="primary" @click="getDeviceSyncFunc">获取oaid</button>

			<button type="primary" @click="deleteDeviceInfo">清空</button>

		</view>

		<view class="version">
			当前版本：{{version}}
		</view>

		<view class="devices">
			设备信息：{{deviceInfo1}}
		</view>

		<view class="devices">
			设备信息：{{deviceInfo2}}
		</view>

	</view>
</template>

<script>
	const mittModule = uni.requireNativePlugin('MiitModule');

	export default {
		data() {
			return {
				title: 'msa',
				deviceInfo1: 'Hello',
				deviceInfo2: 'Hello',
				deviceInfo3: 'Hello',
				deviceInfo4: 'Hello',
				version: ''
			}
		},
		onLoad() {
			// #ifdef APP-PLUS
			this.version = plus.runtime.version;
			// #endif
		},
		methods: {
	
			testAsyncFunc() {
				mittModule.getAsyncFunc((ret) => {
					this.deviceInfo1 = "support:" + ret.support +
						"  \nisLimited:" + ret.isLimited +
						"\noaid:" + ret.oaid;
				});
			},
			getDeviceSyncFunc() {
				// 调用同步方法
				mittModule.getDeviceSyncFunc((ret) => {
					this.deviceInfo2 = "support:" + ret.support +
						"  \nisLimited:" + ret.isLimited +
						"\noaid:" + ret.oaid;
					console.log("ret:" + ret)
				});

			},
			deleteDeviceInfo() {
				this.deviceInfo1 = ""
				this.deviceInfo2 = ""
			},
		}
	}
</script>

<style>
	.about {
		flex-direction: column;
		flex: 1;
	}

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

	button {
		width: 100%;
		margin-top: 40rpx;
	}

	.devices {
		width: 200rpx;
		margin-top: 40rpx;
		justify-content: center;
		color: #444;
	}

	.device4 {
		width: 200rpx;
		margin-top: 40rpx;
		padding-bottom: 40rpx;
		justify-content: center;
		color: #444;
	}



	.version {
		height: 80rpx;
		line-height: 80rpx;
		justify-content: center;
		color: #ccc;
	}
</style>
