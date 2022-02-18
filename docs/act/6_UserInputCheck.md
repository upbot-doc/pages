---
sort: 6
---

# 文本检测

## 基本信息

**Path：** /api/act/UserInputCheck

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
| word        | string  | 非必须   |     | 待检测文本     | word和words同时存在时，只检测words字段  |
| ts          | integer | 必须   |     | 时间戳            |                 |
| nonce       | string  | 必须   |     | 随机字符串          |                 |
| words       | string []  | 非必须   |     | 待检测文本列表     | 批量检测，最多支持10条  |
| openid       | string | 必须   |     | 字符串类型的uid     |                 |
| activity_id  | string | 非必须   |     | 活动ID | 拼接而成的字符串，能够通过此ID定位到内容，例如：{bot_id}-{gid}-{vote_id}  |

### 示例
```json
{
    "ts": 1641006865,
    "nonce": "nonce",
    "word": "文本内容",
    "activity_id": "1000009828-10123-1021"
}
```
或
```json
{
    "ts": 1641006865,
    "nonce": "nonce",
    "words": ["文本内容1","文本内容2"]
}
```


## 返回数据

| 名称                     | 类型      | 是否必须 | 默认值 | 备注     | 其他信息             |
|------------------------|---------|------|-----|--------|------------------|
| ret                    | integer | 必须   |     |       |                  |
| msg                    | string  | 必须   |     |       |                  |
| result                   | object  | 非必须  |     |        | {}               |
| ├─ level               | integer | 必须  |     | 风险等级 |        0无风险 1有风险          |
| ├─ message             | string | 必须  |     | 风险提示 | 仅做提示使用，不可用于逻辑判断     |

### 示例
```json
{
    "ret": 0,
    "msg": "ok",
    "result": {
        "level": 0,
        "message": "PASS"
    }
}
```