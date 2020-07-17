<template>
	<view class="content">
		<view class="btns">
			<button class="btn" @click="checkByPrivateFilePath">checkByPrivateFilePath</button>
			<button class="btn" @click="checkByOriginApkPackageName">checkByOriginApkPackageName</button>
			<button class="btn" @click="checkByMultiApkPackageName">checkByMultiApkPackageName</button>
			<button class="btn" @click="checkByHasSameUid">checkByHasSameUid</button>
			<button class="btn" @click="checkByPortListening">checkByPortListening</button>
			<button class="btn" @click="checkIsRunningInVirtualApk">checkIsRunningInVirtualApk</button>
			<button class="btn" @click="checkIsRoot">checkIsRoot</button>
			<button class="btn" @click="checkIsDebug">checkIsDebug</button>
			<button class="btn" @click="checkIsUsbCharging">checkIsUsbCharging</button>
			<button class="btn" @click="checkIsDebuggerConnected">checkIsDebuggerConnected</button>
			<button class="btn" @click="checkIsBeingTracedByC">checkIsBeingTracedByC</button>
			<button class="btn" @click="checkIsXposedExist">checkIsXposedExist</button>
			<button class="btn" @click="checkIsRunningInEmulator">checkIsRunningInEmulator</button>
		</view>
		
		
		<view class="out_wrap">
			<text class="out">{{ out }}</text>
		</view>
		
	</view>
</template>

<script>
	const easyProtector = uni.requireNativePlugin('easy-protector');
	
	export default {
		data() {
			return {
				title: 'Hello',
				out: "",
			}
		},
		
		onLoad() {
			this.log("easyProtector exist" + JSON.stringify(easyProtector))
		},
		
		methods: {
			
			checkByPrivateFilePath(){
				let ret = easyProtector.checkByPrivateFilePath();
				this.log("checkByPrivateFilePath：" + ret);
			},
			
			checkByOriginApkPackageName(){
				let ret = easyProtector.checkByOriginApkPackageName();
				this.log("checkByOriginApkPackageName：" + ret);
			},
			
			/**
			 * 运行被克隆的应用，该应用会加载多开应用的so库
			 * 检测已经加载的so里是否包含这些应用的包名
			 */
			checkByMultiApkPackageName(){
				let ret = easyProtector.checkByMultiApkPackageName();
				this.log("checkByMultiApkPackageName：" + ret);
			},
			
			 /**
			  * Android系统一个app一个uid
			  * 如果同一uid下有两个进程对应的包名，在"/data/data"下有两个私有目录，则该应用被多开了
			  */
			checkByHasSameUid(){
				let ret = easyProtector.checkByHasSameUid();
				this.log("checkByHasSameUid：" + ret);
			},
			
			/**
			 * 端口监听，先扫一遍已开启的端口并连接，
			 * 如果发现能通信且通信信息一致，
			 * 则认为之前有一个相同的自己打开了（也就是被多开了）
			 * 如果没有，则开启监听
			 * 这个方法没有 checkByCreateLocalServerSocket 方法简单，不推荐使用
			 */
			checkByPortListening(){
				easyProtector.checkByPortListening();
				this.log("checkByPortListening：call");
			},
			
			checkIsRunningInVirtualApk(){
				let ret = easyProtector.checkIsRunningInVirtualApk();
				this.log("checkIsRunningInVirtualApk：" + ret);
			},
			
			checkIsRoot(){
				let ret = easyProtector.checkIsRoot();
				this.log("checkIsRoot：" + ret);
			},
			
			checkIsDebug(){
				let ret = easyProtector.checkIsDebug();
				this.log("checkIsDebug：" + ret);
			},
			
			checkIsUsbCharging(){
				let ret = easyProtector.checkIsUsbCharging();
				this.log("checkIsUsbCharging：" + ret);
			},
			
			checkIsDebuggerConnected(){
				let ret = easyProtector.checkIsDebuggerConnected();
				this.log("checkIsDebuggerConnected：" + ret);
			},
			
			checkIsBeingTracedByC(){
				easyProtector.checkIsBeingTracedByC();
				this.log("checkIsBeingTracedByC：call");
			},
			
			/**
			 * 检测Xposed是否存在
			 */
			checkIsXposedExist(){
				let ret = easyProtector.checkIsXposedExist();
				this.log("checkIsXposedExist：" + ret);
			},
			
			/**
			 * 检测模拟器环境
			 * 
			 * suspectCount 为嫌疑值，值越大模拟器的嫌疑越高
			 */
			checkIsRunningInEmulator(){
				easyProtector.checkIsRunningInEmulator((ret)=>{
					this.log("checkIsRunningInEmulator：" + ret);
				});
			},
			
			
			
			
			
			log(text){
				let now = new Date();
				let time = now.getHours() + ":" + now.getMinutes() + ":" + now.getSeconds();
				this.out = (time+": "+text) +"\n\n"+ this.out;
			},
		}
	}
</script>

<style lang="scss" scoped>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		
		
		.btns{
			margin-top: 40rpx;
			display: flex;
			flex-wrap: wrap;
			
			.btn{
				width: 350rpx;
				height: 70rpx;
				font-size: 20rpx;
				margin-bottom: 20rpx;
				display: flex;
				justify-content: center;
				align-items: center;
			}
		}
		
		.out_wrap{
			width: 750rpx;
			height: 400rpx;
			position: absolute;
			left: 0;
			bottom: 0;
			
			display: flex;
			justify-content: center;
			align-items: center;
			background: #282c35;
			
			.out{
				width: 690rpx;
				height: 100%;
				overflow: scroll;
				
				font-size: 25rpx;
				color: #FFFFFF;	
				word-break: break-all;
				margin-top: 30rpx;
			}
		}
		
		
	}
</style>
