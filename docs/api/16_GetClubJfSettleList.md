---
sort: 16
---

# 获取积分结算信息

## 接口描述

**Path：** /upbot/api/GetClubJfSettleList

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
| source              |     integer    |   否   |       |  来源。由于 0 也是其中一种来源类型，这里约定传 -1 表示查询所有来源                                        |                                                         |
| start_time_unix_sec              |     integer    |   否   |       |  开始时间，unix时间戳，单位 秒                                        |                                                         |
| end_time_unix_sec              |     integer    |   否   |       |  结束时间，unix时间戳，单位 秒                                        |                                                         |
| page_context        |     string    |   否   |       | 首次不用传，之后页都用当前请求结果页                                        |                                                         |

## 请求示例
```
{
    "openid": "xxxxd3dd",
    "page_context": "1279"
}
```

## 返回数据

|                名称              |           类型         | 是否必须 | 默认值 |       备注                                 |    其他信息     |
|----------------------------------|-----------------------|----------|-------|--------------------------------------------|----------------|
| ret                              |  integer              |   必须   |        |                                           |                |
| msg                              |  string               |    否    |  空串  |                                           |                |
| data                             |  object               |   必须   |        |     返回数据                              |               |
| ├─  settle_list                  |  array         |   必须   |        |  结算列表                          |               |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  billno  |  string    | 必须   |     | 订单ID，最长64字节     |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  amt  |   integer  | 必须   |     |   交易金额     |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  settle_amt  |   double  | 必须   |     |   结算金额，保留两位小数     |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  amt_ratio  |   integer  | 必须   |     |   结算金额百分比。  范围[0, 100]   |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  settle_time  |   integer  | 必须   |     |   结算时间，unix时间戳，精确到毫秒     |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  account  |   object  | 否   |     |   积分订单的账号信息     |          |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ├─  type  |   integer  | 否   |     |   账号类型，1用户 2俱乐部     |          |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ├─  id  |   string  | 否   |     |   用户openid或则俱乐部ID     |          |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ├─  gid  |   integer  | 否   |     |   游戏ID     |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  detail  |   string  | 必须   |     |   订单详情     |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  source  |   integer  | 必须   |     |   积分来源     |          |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─  jf_gid  |   integer  | 必须   |     |   积分所属游戏     |          |
| ├─  total_amt                  |  double         |   必须   |        |  总计金额。查询条件内的总计结算金额，仅展示用，保留两位小数。只在第一次查询时返回（req 的 page_context 为空时）                          |               |
| ├─  page_context                  |  string         |   必须   |        |  分页信息，透传获取下一页                          |               |
| ├─  is_end                        |  bool         |   必须   |        |  是否没有数据了                          |               |


| source取值    | 说明    |
|----------------------|------------|
|  0	|其他(+/-)             |
 |  1	|充值(+)               |
 |  2	|道具购买(+)            |
 |  3	|三卡购买(+)            |
 |  4	|服务购买(+)            |
 |  5	|活动(+/-)             |
 |  6	|赛事(+/-)             |
 |  7	|捐赠(+/-)             |
 |  8	|兑换(-)               |
 |  9	|过期(-)               |
  | 10	|活跃(+)               |
  | 11	|回滚(+/-)             |
  | 12	|约战(+/-)             |
  | 13	|组队(+/-)             |
  | 14	|游戏家联盟(+/-)        |
  | 15	|悬赏广场(+/-)          |
  | 16	|活动工具(+/-)          |

## 成功响应
```
{
    "ret": 0,
    "msg": "",
    "data": {
        "settle_list": [{
            "billno": "3243434",
            "amt": 2000,
            "settle_amt"： 1.34,
            "amt_ratio": 20,
            "settle_time": 1713147090,
            "account": {
                "type": 1,
                "id": "3dsf34efrefg",
                "gid": 1279
            },
            "detail": "活动",
            "source": 14,
            "jf_gid": 1279
        }],
        "page_context": "122",
        "is_end": false,
        "total_amt": 88888.33
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

