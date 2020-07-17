> 本插件基于知名开源Android检测刷子党库EasyProtector封装

EasyProtector Github地址：https://github.com/lamster2018/EasyProtector



### 体验检测能力

安装Demo的Apk，快速体验检测能力

链接下载：https://github.com/fengerwoo/EasyProtectorDemo/raw/master/unpackage/debug/android_debug.apk

扫码下载

![扫码下载](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggtswj3610j30b40b4jrj.jpg'扫码下载')



拥有羊毛党、模拟器、是否root、Xposed、多开环境等等十多项检测能力

方法快速一览
- checkByPrivateFilePath
- checkByOriginApkPackageName
- checkByMultiApkPackageName
- checkByHasSameUid
- checkByPortListening
- checkIsRunningInVirtualApk
- checkIsRoot
- checkIsDebug
- checkIsUsbCharging
- checkIsDebuggerConnected
- checkIsBeingTracedByC
- checkIsXposedExist
- checkIsRunningInEmulator







### 快速上手



##### 安装原生插件

点击右侧使用HbuilderX 导入插件按钮，然后导入到自己想要使用的项目

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggtt6jxkwqj30gk034q31.jpg)

manifest.json -> App原生插件配置 ->云端插件 选择EasyProtector



##### 导入EasyProtector插件
```javascript
const easyProtector = uni.requireNativePlugin('easy-protector');
```



##### 使用EasyProtector插件

```javascript
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
```



##### 完整Demo下载

Github地址：https://github.com/fengerwoo/EasyProtectorDemo



##### 加入交流群

扫码加我微信加入微信交流群



<img src="https://tva1.sinaimg.cn/large/007S8ZIlgy1ggttzj6g2kj30fo0fqdhs.jpg" style="zoom:33%;" />