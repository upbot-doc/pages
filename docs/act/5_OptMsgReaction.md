---
sort: 5
---

# 操作表态消息

## 基本信息

**Path：** /api/act/OptMsgReaction

**Method：** POST

**接口描述：**

## 请求参数

### Headers

| 参数名称          | 参数值              | 是否必须 | 示例 | 备注 |
|---------------|------------------|------|----|----|
| Content-Type  | application/json | 是    |    |    |
| Authorization | token            | 是    |    |    |

### Body

| 名称          | 类型      | 是否必须 | 默认值 | 备注             | 其他信息            |
|-------------|---------|------|-----|----------------|-----------------|
| opt         | integer | 必须   |     | 操作类型 1 增加｜2 删除 |                 |
| msg_seq     | integer | 必须   |     | 消息序列号          |                 |
| channel_id  | string  | 必须   |     | 频道ID，字符串类型     |                 |
| reaction_id | integer | 必须   |     | 表态ID           |                 |
| l2_type     | integer | 必须   |     | 消息类型           | msg_seq的l2_type |
| ts          | integer | 必须   |     | 时间戳            |                 |
| nonce       | string  | 必须   |     | 随机字符串          |                 |

### 示例
```json
{
    "ts": 1641006865,
    "nonce": "nonce",
    "opt": 1,
    "msg_seq": 463,
    "channel_id": "22658",
    "reaction_id": 100,
    "l2_type": 1
}
```

## 返回数据

| 名称                     | 类型      | 是否必须 | 默认值 | 备注     | 其他信息             |
|------------------------|---------|------|-----|--------|------------------|
| ret                    | integer | 必须   |     |       |                  |
| msg                    | string  | 必须   |     |       |                  |


### 示例
```json
{
    "ret": 0,
    "msg": "ok"
}
```