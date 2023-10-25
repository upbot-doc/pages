---
sort: 7
---

# 查询用户积分收支记录

## 接口描述

**Path：** /upbot/api/GetUserClubPointsList

**Method：** POST


## 请求参数

### Headers

| 参数名称          | 参数值              | 是否必须 | 示例 | 备注 |
|---------------|------------------|------|----|----|
| Content-Type  | application/json | 是    |    |    |
| Authorization | token            | 是    |    |    |

### Body

| 名称                   | 类型         | 是否必须 | 默认值 | 备注                        | 其他信息                                         |
|----------------------|------------|------|-----|---------------------------|----------------------------------------------|
| openid                  | string    | 必须   |     | 心悦openid                    |                                              |
| start_time                  | integer    | 否   |  0   | 查询积分起始时间（毫秒）                    |                                              |
| end_time                  | integer    | 否   |   0  | 查询积分结束时间（毫秒）                    |                                              |
| page                  |   integer  | 否   |  1   | 分页页码                    |                                              |
| page_size                  | integer    | 否   |  10   | 分页大小                    |                                              |


## 请求示例
```
{
    "openid": "JHhd993hGG8n0dsfn9hhsdhfi",
    "start_time": 123343434,
    "end_time": 123343434,
    "page": 1,
    "page_size": 10
}
```

## 返回数据

| 名称  | 类型      | 是否必须 | 默认值 | 备注 | 其他信息          |
|-----|---------|------|-----|----|---------------|
| ret | integer | 非必须  |     |    |  |
| msg | string  | 非必须  |     |    |               |
| data | object  | 非必须  |     |   数组 |               |
| ├─ list | array  | 非必须  |     |   数组 |               |
|   ├─ bill_type          | integer    | 非必须  |     | 交易类型 1:增加 2：减少             |                                              |
|   ├─ amount        | string    | 非必须  |     | 积分数量              |                                              |
|   ├─ create_time      | string    | 非必须  |     |  创建时间，unix时间戳，精确到毫秒              |                                              |                
|   ├─ desc      | string    | 非必须  |     | 积分描述              |                                              |                
| ├─ total          | integer    | 非必须  |     | 总数量              |                                              |


## 成功响应
```
{
    "ret": 0,
    "msg": "",
    "data": {
        "list": [{
            "bill_type": 1,
            "amount": 100,
            "create_time": 123467677,
            "desc": 完成任务奖励积分
        }],
        "total": 23
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

