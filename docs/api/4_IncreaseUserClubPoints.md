---
sort: 4
---

# 增加用户俱乐部个人积分

## 接口描述

**Path：** /upbot/api/IncreaseUserClubPoints

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
| bill_no                  | string    | 必须   |     | 交易订单id。必填，最长64字节                    |                                              |
| charge_list                  | array    | 必须   |     | 需要操作的积分列表                    |                                              |
| ├─ openid | string  | 必须  |     |   用户openid |               |
| ├─ amount | integer  | 必须  |     |   积分数量 |               |
| ├─ expired_time | integer  | 非必须  |     |   过期时间(秒)，unix时间戳，默认是一年。 |               |
| desc                  | string    | 必须   |     | 积分变更说明                    |                                              |
| gid                  | integer    | 否   |     | 游戏id                    |                                              |

## 请求示例
```
{
    "bill_no": "dfg34dfgfg4sdgsdfdsfsdf3",
    "charge_list": [{
        "openid": "JHhd993hGG8n0dsfn9hhsdhfi",
        "amount": 100,
        "expired_time": 123434545455
    }],
    "desc": "完成任务奖励积分",
    "gid": 1279
}
```

## 返回数据

| 名称  | 类型      | 是否必须 | 默认值 | 备注 | 其他信息          |
|-----|---------|------|-----|----|---------------|
| ret | integer | 非必须  |     |    |  |
| msg | string  | 非必须  |     |    |               |


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

