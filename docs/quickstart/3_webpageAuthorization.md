---
sort: 3
---

# 网页授权

如果用户想访问心悦upbot资源，可以通过心悦网页授权机制，来获取用户基本信息，进而实现业务逻辑。

## 网页授权回调域名

开发者需要提供安全域名，做为需要网页授权的域名。

请注意，这里填写的是域名（是一个字符串），而不是URL，因此请勿加 http:// 等协议头。

## 开发说明

1. 开发者在获取用户信息后，可以通过Cookie或Session机制等，转换为自己的登陆校验机制，无须每次打开页面都执行授权流程。

## 网页授权流程

### 1 获取code

1. 绑定域名，与心悦沟通，获取app_id
2. 引入js文件
3. 设置环境（正式or测试）
```html
<!-- 测试环境 -->
<script src="https://xinyue.qq.com/dev/XYTeam/auth3rdSdk/index.min.js"></script>
<!-- 预发布环境环境 -->
<script src="https://xinyue.qq.com/pre/XYTeam/auth3rdSdk/index.min.js"></script>
<!-- 正式环境(latest) -->
<script src="https://xinyue.qq.com/XYTeam/auth3rdSdk/index.min.js"></script>
<!-- 正式环境 1.0.0 -->
<script src="https://xinyue.qq.com/XYTeam/auth3rdSdk/1.0.0/index.min.js"></script>
```
4. 获取鉴权code
```javascript
const { ret, state, code, isNewUser, mcnUid } = await window.auth3rdSdk.Auth({
  appId: '', // 必填
  redirectUrl: '', // 可选，授权后跳转页面，不传默认为回当前页面
});
if (code) {
    // 当前已授权，获取成功
} else {
    // 当前未授权，将自动跳转授权
}
```

注：Auth方法闭环获取鉴权过程，调用该方法获取参数即可，获取失败时会根据传入参数决定是否拉起登录/授权

重定向参数 ret, state, tgclubCode, useLogin, mcnUid，Auth内会进行映射

#### 说明
##### （1）授权/登录（异步方法）
##### 方法名：Auth
##### 入参：object
```ts
{
  appId: string, // 必填，后台校验用
  useLogin: boolean, // 可选，用于判断当前是使用授权功能还是使用心悦登录，默认false
  // 授权：当前游戏家已登录，但未绑定心悦账号
  // 登录：当前游戏家未登录，选择心悦渠道登录
  redirectUrl: string, // 可选，授权后跳转页面，不传默认为回当前页面
  autoLoginNewUser: boolean, // 新用户是否自动跳转登录，默认true
}
```
##### 返回：object
```ts
{
  ret: number, // 状态码 0 正常 -1 异常
  state: string, // 随机数，相当于CSRF token 状态码为0时返回
  code: string, // 授权码 状态码为0时返回
  isNewUser: boolean, // 是否是新用户，useLogin为true时返回
  mcnUid: string, // 游戏家联盟用户id，useLogin为true时返回
}
```
##### 调用示例
```javascript
const { ret, state, code, isNewUser, mcnUid } = window.auth3rdSdk.Auth({
  appId: '', // 必填
  redirectUrl: '', // 可选，授权后跳转页面，不传默认为回当前页面
});
if (code) {
    // 当前已授权，获取成功
} else {
    // 当前未授权，将自动跳转授权
}
```
说明：请求参数为object，已授权返回code，未授权返回空字符串，并拉起心悦授权

##### （2）获取当前平台
##### 常量：PLATFROM
```ts
{
  QQ: string, // qq
  WECHAT: string, // 微信
  BROWSER: string, // 浏览器
  TGCLUB: string, // 心悦APP
};
```
##### 调用示例
```js
const { PLATFROM, platform } = window.auth3rdSdk;
if (platform === PLATFROM.TGCLUB) {
  // 心悦内
}
```


### 2 通过code换取网页授权access_token

**Path：** /upbot/api/auth/GetAccessToken

**Method：** POST

**Headers**

| 参数名称          | 参数值              | 是否必须 | 示例 | 备注 |
|---------------|------------------|------|----|----|
| Content-Type  | application/json | 是    |    |    |

**参数说明：**

| 名称         | 类型     | 是否必须 | 默认值 | 备注                     | 其他信息         |
|------------|--------|------|-----|------------------------|--------------|
| appid      | string | 必须   |     | 应用唯一凭证                |  |
| app_secret | string | 必须   |     | 应用唯一凭证密钥             |          |
| code       | string | 必须   |     | 填写第一步获取的code参数         |    有效期5分钟，只能使用一次          |
| grant_type | string | 必须   |     | 填写为 authorization_code |              |

**返回说明：**

| 名称                | 类型      | 是否必须 | 默认值 | 备注                          | 其他信息                    |
|-------------------|---------|------|-----|-----------------------------|-------------------------|
| ret               | integer | 必须   | 0   |                             |                         |
| msg               | string  | 必须   | ok  |                             |                         |
| data         | object  |      |     | 授权信息                        |                         |
| ├─ access_token   | string  |      |     | 网页授权接口调用凭证                  |                         |
| ├─ expires_in     | number  |      |     | access_token接口调用凭证超时时间，单位（秒 |                         |
| ├─ refresh_token  | string  |      |     | 用户刷新access_token,有效期30天     |                         |
| ├─ openid         | string  |      |     | 用户唯一标识                      | uid 字符串类型               |
| ├─ scope          | string  |      |     | 作用域                         | 目前会固定返回openapi_userinfo |

### 3 拉取用户信息(需scope为 openapi_userinfo)

**Path：** /upbot/api/auth/UserInfo

**Method：** POST

**参数说明：**

| 名称           | 类型     | 是否必须 | 默认值 | 备注         | 其他信息      |
|--------------|--------|------|-----|------------|-----------|
| access_token | string | 必须   |     | 网页授权接口调用凭证 |           |
| openid       | string | 必须   |     | 用户唯一标识     | uid 字符串类型 |

**返回说明：**

| 名称          | 类型      | 是否必须 | 默认值 | 备注     | 其他信息      |
|-------------|---------|------|-----|--------|-----------|
| ret         | integer | 必须   | 0   |        |           |
| msg         | string  | 必须   | ok  |        |           |
| data   | object  |      |     | 用户信息   |           |
| ├─ openid   | string  |      |     | 用户唯一标识 | uid 字符串类型 |
| ├─ nick_name | string  |      |     | 用户群昵称  |           |
| ├─ avatar   | string  |      |     | 用户头像   |           |


### 4 刷新access_token（如果需要）

**Path：** /upbot/api/auth/RefreshToken

**Method：** POST

**参数说明：**

| 名称            | 类型     | 是否必须 | 默认值 | 备注                                 | 其他信息        |
|---------------|--------|------|-----|------------------------------------|-------------|
| appid      | string | 必须   |     | 应用唯一凭证                |  |
| refresh_token | string | 必须   |     | 填写通过AccessToken获取到的refresh_token参数 |             |
| grant_type    | string | 必须   |     | 填写为 refresh_token                  |             |

**返回说明：**

| 名称                | 类型      | 是否必须 | 默认值 | 备注                          | 其他信息                    |
|-------------------|---------|------|-----|-----------------------------|-------------------------|
| ret               | integer | 必须   | 0   |                             |                         |
| msg               | string  | 必须   | ok  |                             |                         |
| data         | object  |      |     | 授权信息                        |                         |
| ├─ access_token   | string  |      |     | 网页授权接口调用凭证                  |                         |
| ├─ expires_in     | number  |      |     | access_token接口调用凭证超时时间，单位（秒 |                         |
| ├─ refresh_token  | string  |      |     | 用户刷新access_token,有效期30天     |                         |
| ├─ openid         | string  |      |     | 用户唯一标识                      | uid 字符串类型               |
| ├─ scope          | string  |      |     | 作用域                         | 目前会固定返回openapi_userinfo |

## 小程序授权流程

跳转方法见小程序开发文档：https://developers.weixin.qq.com/miniprogram/dev/api/navigate/wx.navigateToMiniProgram.html

参数均放在 extraData，通过onShow获取。

> 心悦小程序APPID和授权页路径申请授权时由开发提供

### 第三方小程序提供参数

```ts
{
  appId: string, // 必填，后台校验用，与h5一致
  useLogin: boolean, // 可选，用于判断当前是使用授权功能还是使用心悦登录，默认false
}
```

### 授权小程序返回参数

```ts
{
  ret: number, // 状态码 0 正常 -1 异常
  state: string, // 随机数，相当于CSRF token 状态码为0时返回
  code: string, // 授权码 状态码为0时返回
  isNewUser: boolean, // 是否是新用户，useLogin为true时返回
  mcnUid: string, // 游戏家联盟用户id，useLogin为true时返回
}
```