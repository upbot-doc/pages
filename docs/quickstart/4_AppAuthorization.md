---
sort: 4
---


# 第三方APP授权SDK
## 注册应用
注册应用需要提供的参数:
●secheme: 用于授权成功后拉起APP；不要与APP主页面secheme重复，尽量使用纯小写字母和数字，避免使用大写字母和特殊符号。仅提供协议头的纯字符串，无需"://xxx"格式内容
●bundleId: 接入SDK的apk包名

注册应用后，心悦返回：
●appId: 心悦俱乐部提供的唯一的appId

## APP接入
### 引入依赖
在gradle引入aar包

### 注册Activity
在AndroidMeanifest.xml中注册授权响应Activity
```
    <activity
        android:name="com.tencent.tgclubsdk.TgAuthActivity"
        android:exported="true"
        android:launchMode="singleTask"
        android:noHistory="true">
        <intent-filter>
            <action android:name="android.intent.action.VIEW" />

            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />

            <data android:scheme="${注册应用时提供的secheme}" />
        </intent-filter>
    </activity>
```

### 初始化SDK
在Application的onCreate生命周期初始化SDK
```
class MyApp : Application() {
    override fun onCreate() {
        super.onCreate()
        val tgApi = TgApiFactory.createTgAPI(this,appId)
        tgApi?.init(this, object : TgHandler() {
            override fun onResp(resp: TgResp?) {
                // 成功处理
                uniquID = 
            }

            override fun onError(code: Int, msg: String) {
                // 失败处理
            }

            override fun onCancel() {
                // 用户取消
            }
        })

    }
}
```

### 请求授权
在需要授权的时候，发送授权请求
```
val tgApi = TgApiFactory.createTgAPI(this, appId)
val req = TgReq()
req.scheme = "${注册应用时提供的secheme}"
tgApi?.sendReq(req)
```

## 错误码
SDK相关错误码看查看TgCode类
|                错误码              |           含义         | TgCode常量 | 备注 |   
|----------------------------------|-----------------------|----------|-------|
| 0                              |  成功              |   SUCCESS   |    通用错误码    |
| -1                              |  未知错误               |    UNKNOWN    |  通用错误码  |
| -2                              |  SDK未初始化               |    NOT_INIT    |  sendReq返回  |
| -3                              |  sendReq参数错误               |    ERROR_PARAMS    |  sendReq返回  |
| -4                              |  心悦APP未安装               |    APP_NOT_INSTALLED    |  sendReq返回  |
| -5                              |  非心悦APP的回调               |    ERROR_REFERRER    |  TgHandler.onError  |
| -6                              |  响应处理错误               |    ERROR_RESPONSE    |  TgHandler.onError  |
| -11                              |  心悦APP授权失败               |    AUTH_FAILED    |  TgHandler.onError  |
| -12                              |  用户取消授权               |    USER_CANCEL    |  TgHandler.onError  |
| -13                              |  心悦APP内部错误               |    -    |  TgHandler.onError的msg ret中  |
| -14                              |  授权SDK内部错误               |    -    |  TgHandler.onError的msg ret中  |
| 其他                              |  透传的后台错误               |    -    |  TgHandler.onError的msg ret中  |



### Q&A
●为什么要在Application的onCreate生命周期注册响应，而不是sendReq的时候注册？
○因为心悦APP授权的过程中，业务APP有可能已被系统或用户kill，此时在重新拉起业务APP，不会走到sendReq逻辑，只有Application的生命周期是必走的

●如何获取心悦授权SDK打印的流程日志？
○TgLog.getLogFile()方法可以拿到最新的日志文件。如果日志比较早，后续打印的日志已超过1M,则可以通过TgLog.getLogBakFile()方法获取；如果TgLog.getLogBakFile()日志也超出1M,则旧日志文件已被清理。
○流程结束，可以调用TgLog.close()释放协程资源。不过释放之后，有可能导致后续流程日志未记录，释放需谨慎

●如何请求心悦测试环境授权页？
○tgApi?.init()方法里，设置isDebug参数为true
