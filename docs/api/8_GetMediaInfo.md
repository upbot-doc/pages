---
sort: 8
---

# 获取私域媒介信息

## 接口描述

**Path：** /upbot/api/GetMediaInfo

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
| account_info                  | object    | 必须   |     | 账号信息                    |                                              |
| ├─  account_type  |  integer   | 必须   |     | 账号类型， 见account_type取值     |          |
| ├─  appid  |   string  | 必须   |     |   应用id     |          |
| ├─  openid  |   string  | 必须   |     |   openid     |          |
| media_type                  | integer    | 必须   |    | 媒介类型，见media_type取值      |             |
| code                  | string    | 必须   |    | 活码         |              |
| trace_id              |   string  | 必须   |    | 跟踪标识,同一次操作保持一致   |       ||

| account_type取值    | 说明    |
|----------------------|------------|
|  1 | QQ |
|  2 | 微信openid |
|  3 | QQ openid |

| media_type取值    | 说明    |
|----------------------|------------|
|  2 | 企业微信群 |


## 请求示例
```
{
    "account_info": {
        "account_type": 2,
        "appid": "xxxx",
        "openid": "xxxx"
    },
    "media_type": 2,
    "code": "IsFXtWUZ3x3hywGl ",
    "trace_id": "Fi6JoptoXX8EI3sttq3pcVGC2H1Nesy9"
}
```

## 返回数据

| 名称  | 类型      | 是否必须 | 默认值 | 备注 | 其他信息          |
|-----|---------|------|-----|----|---------------|
| ret | integer |   |     |    |  |
| msg | string  |   |     |    |               |
| data | object  |   |     | 数据 |               |
| ├─ url | string  |   |     |   加群链接 |               |
| ├─ name          | string    |   |     | 媒介名称             |                                              |
| ├─ background        | string    | 否 |     |  背景图              |                                              ||


## 成功响应
```
{
    "ret": 0,
    "msg": "",
    "data": {
        "url": "xxxxx",
        "name": "火影忍者-聊天俱乐部",
        "background": ""
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

