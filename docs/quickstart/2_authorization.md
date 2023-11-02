---
sort: 2
---

# 开发入门

## 接口调用凭证
>接口应在服务器端调用

### 接口英文名
getAccessToken

####功能描述

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
