---
sort: 2
---

# 开发入门

## 接口调用凭证
>接口应在服务器端调用

### 接口英文名
getAccessToken

#### 功能描述

获取心悦全局唯一后台接口调用凭据，token有效期为7200s，开发者需要进行妥善保存。
为了 access_token 的安全性，开发者应在后端服务器使用getAccessToken获取 access_token，并调用相关 API；
请求所有的API时，我们需要在 http header 添加鉴权字段，格式为 `Authorization: TOKEN`。

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
| grant_type | string | 必须   |     | 填写为 client_credentials |              |
| scope | string | 否   |     |  |              |

**返回说明：**

| 名称                | 类型      | 是否必须 | 默认值 | 备注                          | 其他信息                    |
|-------------------|---------|------|-----|-----------------------------|-------------------------|
| ret               | integer | 必须   | 0   |                             |                         |
| msg               | string  | 必须   | ok  |                             |                         |
| data         | object  |      |     | 授权信息                        |                         |
| ├─ access_token   | string  |      |     | 网页授权接口调用凭证                  |                         |
| ├─ expires_in     | number  |      |     | access_token接口调用凭证超时时间，单位（秒 |                         |
| ├─ refresh_token  | string  |      |     | 用户刷新access_token,有效期30天     |                         |
| ├─ scope          | string  |      |     | 作用域                         |  |



## 成功响应
```
{
    "ret":0,
    "msg":"ok",
    "data":{
        "access_token":"b7305db37f292d4efdfdc15b8bbf34d4650169ee78278d2c5f514f90b0e3",
        "expires_in":7200,
        "refresh_token":"7afc58787af5077c8h99ja9b4b58ec018184894a5b001cd53158e3a2c7bd",
        "scope":"openapi_xxxxx"
    }
}
```

## 错误响应
```
{
	"ret": 1001,
	"msg": "请求参数错误，请稍后再试"
}
```


### 其他说明

#### access_token 的存储与更新

access_token 的存储至少要保留 512 个字符空间；
access_token 的有效期目前为 2 个小时，需定时刷新，重复获取将导致上次获取的 access_token 失效；
建议开发者使用中控服务器统一获取和刷新 access_token，其他业务逻辑服务器所使用的 access_token 均来自于该中控服务器，不应该各自去刷新，否则容易造成冲突，导致 access_token 覆盖而影响业务；
access_token 的有效期通过返回的 expires_in 来传达，目前是7200秒之内的值，中控服务器需要根据这个有效时间提前去刷新。在刷新过程中，中控服务器可对外继续输出的老 access_token，此时开放平台后台会保证在5分钟内，新老 access_token 都可用，这保证了第三方业务的平滑过渡；
access_token 的有效时间可能会在未来有调整，所以中控服务器不仅需要内部定时主动刷新，还需要提供被动刷新 access_token 的接口，这样便于业务服务器在API调用获知 access_token 已超时的情况下，可以触发 access_token 的刷新流程。


###  刷新access_token（如果需要）

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
| ├─ scope          | string  |      |     | 作用域                         |  |
