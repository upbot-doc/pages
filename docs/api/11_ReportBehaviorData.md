---
sort: 11
---

# 行为数据上报

## 接口描述

**Path：** /upbot/api/ReportBehaviorData

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
| ├─  uid |  string   | 必须   |     | 用户ID      |
| ├─  openid |  string   | 必须   |     | 心悦openid
| ├─  device_type  |  integer   |  |     | 设备类型:1安卓, 2IOS    |          |
| ├─  business_type  |  integer   |  |     | 业务类型：1游戏家联盟    |          |
| items             |   object  | 必须   |    | 数据内容           |       |
| ├─  event_time  |  integer  |  |     | 事件发生时间戳，时间戳(秒)   |          |
| ├─  channel  |  integer  |  |     | 渠道：1 H5 2小程序   |          |
| ├─  operate_id  |  integer  |  |     | 操作类型   |          |
| ├─  page_id  |  integer  |  |     | 页面ID   |          |
| ├─  pos_id  |  integer  |  |     | 页面位置id   |          |
| ├─  prev_id  |  integer  |  |     | 上级来源页id   |          |
| ├─  trace_id  |  string  | | | 跟踪标识,同一次操作保持一致    | |
| ├─  duration  |  integer  |  |     |  停留时长(秒)  |          |



| operate_id 取值    | 说明    |
|----------------------|------------|
|  10000 | 访问H5页面 |
|  11000 | 访问小程序页面 |

## 请求示例
```
{
    "head": {
        "uid": 890347598,
        "openid": "HH88bB83BB",
        "device_type": 1,
        "business_type": 1
    },
    "items": [{
        "event_time": 1699274742,
        "channel": 1,
        "operate_id": 10000,
        "page_id": 2,
        "pos_id": 2,
        "prev_id": 2,
        "trace_id": "Fi6JoptoXX8EI3sttq3pcVGC2H1Nesy9",
        "duration": 20
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

