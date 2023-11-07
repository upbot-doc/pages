---
sort: 9
---

# 私域事件上报

## 接口描述

**Path：** /upbot/api/ReportMediaEvent

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
| head                  | object    | 必须   |     | 公共信息      |                  |
| ├─  account_info |  object   | 必须   |     | 账号信息      |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  account_type  |  integer   | 必须   |     | 账号类型， 见account_type取值     |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  appid  |   string  | 必须   |     |   应用id     |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─ openid  |   string  | 必须   |     |   openid     |          |
| ├─  device_info     | object    |    |    | 设备信息      |             |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  device_type  |  integer   |  |     | 设备类型:1安卓, 2IOS    |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  uuid  |  string   |  |     | 设备标识    |          |
| item              |   list  | 必须   |    | 数据内容列表           |       |
| ├─ MediaEventItem             |   object  | 必须   |    | 数据内容           |       |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  event_id  |  string   |  |     | 事件ID，见even_id取值   |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  event_time  |  integer  |  |     | 事件发生时间戳，时间戳   |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  media_type  |  integer  |  |     | 媒介类型，见media_type取值   |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  code  |  string  |  |     | 活码   |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  trace_id  |  string  | | | 跟踪标识,同一次操作保持一致    | |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  duration  |  integer  |  |     |  停留时长(秒)  |          |

| account_type取值    | 说明    |
|----------------------|------------|
|  1 | QQ |
|  2 | 微信openid |
|  3 | QQ openid |

| media_type取值    | 说明    |
|----------------------|------------|
|  2 | 企业微信群 |


| event_id取值    | 说明    |
|----------------------|------------|
|  1100102 | 跳转小程序页面 |
|  1110201 | 二维码曝光 |
|  1110204 | 长按识别加群二维码 |

## 请求示例
```
{
    "head": {
        "account_info": {
            "account_type": 2,
            "appid": "xxxx",
            "openid": "xxxx"
        },
        "device_info": {
            "device_type": 1,
            "uuid": "xxxx"
        }
    },
    "items": [{
        "event_id": "1002",
        "event_time": 1699274742,
        "media_type": 2,
        "code": "IsFXtWUZ3x3hywGl ",
        "trace_id": "Fi6JoptoXX8EI3sttq3pcVGC2H1Nesy9"
    }]
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
    "msg": ""
}
```

## 错误响应
```
{
    "ret": 1001,
    "msg": "请求参数错误，请稍后再试"
}
```

