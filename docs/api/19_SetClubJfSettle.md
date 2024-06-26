---
sort: 19
---

# 积分结算。用于结算属于游戏家的积分

## 接口描述

**Path：** /upbot/api/SetClubJfSettle

**Method：** POST


## 请求参数

### Headers

| 参数名称          | 参数值              | 是否必须 | 示例 | 备注 |
|---------------|------------------|------|----|----|
| Content-Type  | application/json | 是    |    |    |
| Authorization | token            | 是    |    |    |    |

### Body
说明：在结算金额小于订单金额的情况下，需要根据情况填写结算金额或者结算金额百分比。都不填则会使用订单金额进行结算
结算金额和百分比只有一个参数会生效，都填优先使用结算金额
最终存储的结算金额为了保证精度会用整数存储，具体业务根据业务需求选择不同方式结算

| 名称                   |      类型      | 是否必须 | 默认值 | 备注                                           | 其他信息                                                 |
|------------------------|---------------|----------|-------|------------------------------------------------|---------------------------------------------------------|
| bill_no                  | string    | 必须   |     | 交易订单id。必填，最长64字节                    |                                              |
| openid              |     string    |   必须   |       | 心悦开平openid                                        |                                                         |
| amt_ratio              |     integer    |   必须   |       | 结算金额百分比。在结算金额小于订单金额的情况下需要传入。范围[0,100]，不填（或者填0）按100%算                                        |                                                         |
| settle_amt              |     integer    |   必须   |       | 结算金额。非 0 时需要小于原订单金额。填写结算金额后，结算百分比默认为 100%                                        |                                                         |

## 请求示例
```
{
    "bill_no": "sdfsdfsdcsdc",
    "openid": "xxxxd3dd",
    "settle_amt": 5000
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