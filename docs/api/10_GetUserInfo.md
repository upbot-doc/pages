---
sort: 10
---

# 查询心悦用户信息

## 接口描述

**Path：** /upbot/api/GetUserInfo

**Method：** POST


## 请求参数

### Headers

| 参数名称          | 参数值              | 是否必须 | 示例 | 备注 |
|---------------|------------------|------|----|----|
| Content-Type  | application/json | 是    |    |    |
| Authorization | token            | 是    |    |    |    |

### Body

| 名称                   | 类型         | 是否必须 | 默认值 | 备注                        | 其他信息                                         |
|----------------------|------------|------|-----|---------------------------|----------------------------------------------|
| account_info |  object   | 必须   |     | 账号信息      |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  account_type  |  integer   | 必须   |     | 账号类型， 见account_type取值     |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  appid  |   string  | 必须   |     |   应用id     |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─ openid  |   string  | 必须   |     |   openid     |          |


| account_type取值    | 说明    |
|----------------------|------------|
|  1 | QQ |
|  2 | 微信openid |
|  3 | QQ openid |


## 请求示例
```
{
    "account_info": {
        "account_type": 2,
        "appid": "xxxx",
        "openid": "xxxx"
    }
}
```

## 返回数据

| 名称  | 类型      | 是否必须 | 默认值 | 备注 | 其他信息          |
|-----|---------|------|-----|----|---------------|
| ret | integer |   |     |    |  |
| msg | string  |   |     |    |               |


## 成功响应
```
{
    "ret": 0,
    "msg": "",
    "data": {"nickname":"心悦用户18AE8","avatar":""}
}
```

## 错误响应
```
{
    "ret": 1001,
    "msg": "请求参数错误，请稍后再试"
}
```

