---
sort: 17
---

# 获取积分结算日统计数据

## 接口描述

**Path：** /upbot/api/GetClubJfSettleDailyStatistic

**Method：** POST


## 请求参数

### Headers

| 参数名称          | 参数值              | 是否必须 | 示例 | 备注 |
|---------------|------------------|------|----|----|
| Content-Type  | application/json | 是    |    |    |
| Authorization | token            | 是    |    |    |    |

### Body

| 名称                   |      类型      | 是否必须 | 默认值 | 备注                                           | 其他信息                                                 |
|------------------------|---------------|----------|-------|------------------------------------------------|---------------------------------------------------------|
| openid              |     string    |   必须   |       | 心悦开平openid                                        |                                                         |
| start_time_unix_sec              |     integer    |   否   |       |  开始日期任意时刻的时间戳，单位 秒。                                        |                                                         |
| end_time_unix_sec              |     integer    |   否   |       |  结束日期任意时刻的时间戳，单位 秒。                                        |                                                         |

## 请求示例
```
{
    "openid": "xxxxd3dd",
    "start_time_unix_sec": 1715067104,
    "end_time_unix_sec": 1715167104
}
```

## 返回数据

|                名称              |           类型         | 是否必须 | 默认值 |       备注                                 |    其他信息     |
|----------------------------------|-----------------------|----------|-------|--------------------------------------------|----------------|
| ret                              |  integer              |   必须   |        |                                           |                |
| msg                              |  string               |    否    |  空串  |                                           |                |
| data                             |  array               |   必须   |        |     返回数据                              |               |
| ├─  user_num                     |  integer         |   必须   |        |  人数                          |               |
| ├─  total_amt                    |  double         |   必须   |        |  总计金额。仅展示用，保留两位小数                          |               |
| ├─  date_unix_sec                |  integer         |   必须   |        |  日期时间戳，单位 秒。当日0点                          |               |


## 成功响应
```
{
    "ret": 0,
    "msg": "",
    "data": [{
        "user_num": 100,
        "total_amt": 10000.12,
        "date_unix_sec": 1714838400
    },{
        "user_num": 20,
        "total_amt": 5454545.88,
        "date_unix_sec": 1714838400
    }]
}
```

## 错误响应
```
{
    "ret": 1001,
    "msg": "请求参数错误，请稍后再试"
}
```