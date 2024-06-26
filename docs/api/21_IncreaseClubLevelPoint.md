---
sort: 21
---

# 添加俱乐部等级分

## 接口描述

**Path：** /upbot/api/IncreaseClubLevelPoint

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
| club_id                  | integer    | 必须   |     | 俱乐部ID                    |                                              |
| bill_no                  | string    | 必须   |     | 发放流水号，唯一标识一次发放，发放按流水号实现幂等，请求超时等重试情况可以使用同一个流水号再次尝试                    |                                              |
| rid                  | string    | 必须   |     | 发放资源id                    |                                              |
| scene                  | string    | 必须   |     |  发放场景值，场景值将用于筛选查询发放历史                    |                                              |
| amount                  | integer    | 必须   |     |  发放份数                    |                                              |
| notes                  | string    | 否   |     |  备注信息，一般为发放页面的title信息                    |                                              |
| flow_time                  | int64    | 必须   |   获取时间戳 秒, 必填  |                      |                                              |
| flow_desc                  | string    | 必须   |   数值变化文案, 必填  |                      |                                              |
| gid                  | string    | 否   |     |  关联游戏ID                    |                                              |
| act_id                  | string    | 否   |     |  关联活动ID                   |                                              |
| remark                  | string    | 否   |     |  备注，仅供内部查看                    |                                              |


## 请求示例
```
{
    "openid": "xxxxd3dd",
    "club_id": 110,
    "bill_no": "1fd297c2-d6a2-4ee7-9179-b612b8471b5820",
    "rid": "A2020011300000111",
    "scene": "gamer-league",
    "amount": 10,
    "notes": "",
    "flow_time": 174958945,
    "flow_desc": "加加加"
}
```

## 返回数据

|                名称              |           类型         | 是否必须 | 默认值 |       备注                                 |    其他信息     |
|----------------------------------|-----------------------|----------|-------|--------------------------------------------|----------------|
| ret                              |  integer              |   必须   |        |                                           |                |
| msg                              |  string               |    否    |  空串  |                                           |                |



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

## 错误码

|                状态码              |           错误信息         |
|----------------------------------|-----------------------|
| 1001	  |   传入的rid无效（常见于资源只发布了测试环境，正式环境未进行发布）                                 |
| 1101	  |   启用了严格校验账户和角色信息，并且传入的信息有缺失                                            |
| 2001	  |   并发的请求使用了重复的流水号                                                              |                       
| 3001	  |   超出资源总限量（msg中会提示超出了日、周、月、总量）                                           |
| 3002	  |   超出单账户限量（msg中会提示超出了日、周、月、总量）                                           |
| 5001	  |   扣减用量时加锁冲突（出现于当前用户并发发放同一资源请求过多，目前极为少见）                         | 
| 5002	  |   当前流水号对应的扣减用量已经被回滚                                                         |
| 5003	  |   当前流水号对应的限量方式配置出现变化 (常出现于，首次调用发放时的限量方式和本次调用的限量方式发生了变化) |