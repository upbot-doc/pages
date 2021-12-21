---
sort: 3
---

# 网页授权（灰度中）

如果用户在KK客户端中，通过Bot访问H5网页，可以通过KK网页授权机制，来获取用户基本信息，进而实现业务逻辑。

## 网页授权回调域名

开发者需要提供安全域名，做为需要网页授权的域名。

请注意，这里填写的是域名（是一个字符串），而不是URL，因此请勿加 http:// 等协议头。

## 开发说明

1. 开发者在获取用户信息后，可以通过Cookie或Session机制等，转换为自己的登陆校验机制，无须每次打开页面都执行授权流程。

## 网页授权流程

### 1 获取code

1. 绑定域名，与bot服务沟通，设置botId及前端域名
2. 引入js文件`https://knock.gtimg.com/web/open/js/knockbot-1.0.0.js`
3. 设置环境（正式or测试）
    ```javascript
    window.knockBotLib.setStage('test'); // 测试环境
    window.knockBotLib.setStage('prod'); // 正式环境
    ```
4. 获取鉴权code
    ```javascript
    window.knockBotLib.authorize({
      appid: '100000', // botId
      redirectUri: 'https://www.noknok.cn', // 回调地址
      responseCode: 'code', // 固定为code
      scope: 'openapi_userinfo', // 固定为openapi_userinfo
      state: Math.floor(Math.random() * 1000000), // 随机数字，回调时会带回来
    });
    ```
5. 等待页面跳回到`redirectUri`，此时会附带`code`参数，`state`参数，如果失败会有`ret`参数，例`https://xxx.com?code=123&state=123&ret=0`

### 2 通过code换取网页授权access_token

**Path：** /web/auth/AccessToken

**Method：** POST

**Headers**

| 参数名称          | 参数值              | 是否必须 | 示例 | 备注 |
|---------------|------------------|------|----|----|
| Content-Type  | application/json | 是    |    |    |

**参数说明：**

| 名称           | 类型     | 是否必须 | 默认值 | 备注                     | 其他信息         |
|--------------|--------|------|-----|------------------------|--------------|
| appid        | string | 必须   |     | 机器人唯一标识                | bot_id字符串类型 |
| secret       | string | 必须   |     | 机器人的secret             | 官方提供         |
| code         | string | 必须   |     | 填写第一步获取的code参数         |              |
| grant_type   | string | 必须   |     | 填写为 authorization_code |              |

**返回说明：**

| 名称                | 类型      | 是否必须 | 默认值 | 备注                          | 其他信息                    |
|-------------------|---------|------|-----|-----------------------------|-------------------------|
| ret               | integer | 必须   | 0   |                             |                         |
| msg               | string  | 必须   | ok  |                             |                         |
| auth_info         | object  |      |     | 授权信息                        |                         |
| ├─ access_token   | string  |      |     | 网页授权接口调用凭证                  |                         |
| ├─ expires_in     | number  |      |     | access_token接口调用凭证超时时间，单位（秒 |                         |
| ├─ refresh_token  | string  |      |     | 用户刷新access_token,有效期30天     |                         |
| ├─ openid         | string  |      |     | 用户唯一标识                      | uid 字符串类型               |
| ├─ scope          | string  |      |     | 作用域                         | 目前会固定返回openapi_userinfo |

### 3 拉取用户信息(需scope为 openapi_userinfo)

**Path：** /web/auth/UserInfo

**Method：** POST

**参数说明：**

| 名称           | 类型     | 是否必须 | 默认值 | 备注         | 其他信息      |
|--------------|--------|------|-----|------------|-----------|
| access_token | string | 必须   |     | 网页授权接口调用凭证 |           |
| openid       | string | 必须   |     | 用户唯一标识     | uid 字符串类型 |
| gid          | number | 必须   |     | 房间ID       |           |

**返回说明：**

| 名称          | 类型      | 是否必须 | 默认值 | 备注     | 其他信息      |
|-------------|---------|------|-----|--------|-----------|
| ret         | integer | 必须   | 0   |        |           |
| msg         | string  | 必须   | ok  |        |           |
| user_info   | object  |      |     | 用户信息   |           |
| ├─ openid   | string  |      |     | 用户唯一标识 | uid 字符串类型 |
| ├─ nickname | string  |      |     | 用户群昵称  |           |
| ├─ avatar   | string  |      |     | 用户头像   |           |
| ├─ gid      | string  |      |     | 房间ID   |           |


### 4 刷新access_token（如果需要）

**Path：** /web/auth/RefreshToken

**Method：** POST

**参数说明：**

| 名称            | 类型     | 是否必须 | 默认值 | 备注                                 | 其他信息        |
|---------------|--------|------|-----|------------------------------------|-------------|
| appid         | string | 必须   |     | 机器人唯一标识                            | bot_id 字符串类型 |
| refresh_token | string | 必须   |     | 填写通过AccessToken获取到的refresh_token参数 |             |
| grant_type    | string | 必须   |     | 填写为 refresh_token                  |             |

**返回说明：**

| 名称                | 类型      | 是否必须 | 默认值 | 备注                          | 其他信息                    |
|-------------------|---------|------|-----|-----------------------------|-------------------------|
| ret               | integer | 必须   | 0   |                             |                         |
| msg               | string  | 必须   | ok  |                             |                         |
| auth_info         | object  |      |     | 授权信息                        |                         |
| ├─ access_token   | string  |      |     | 网页授权接口调用凭证                  |                         |
| ├─ expires_in     | number  |      |     | access_token接口调用凭证超时时间，单位（秒 |                         |
| ├─ refresh_token  | string  |      |     | 用户刷新access_token,有效期30天     |                         |
| ├─ openid         | string  |      |     | 用户唯一标识                      | uid 字符串类型               |
| ├─ scope          | string  |      |     | 作用域                         | 目前会固定返回openapi_userinfo |
