---
sort: 4
---

# 查询用户邀请信息

## 基本信息

**Path：** /api/act/InquireUserInviteRecord

**Method：** POST

**接口描述：**

## 请求参数

### Headers

| 参数名称          | 参数值              | 是否必须 | 示例 | 备注 |
|---------------|------------------|------|----|----|
| Content-Type  | application/json | 是    |    |    |
| Authorization | token            | 是    |    |    |

### Body

| 名称         | 类型      | 是否必须 | 默认值 | 备注                   | 其他信息             |
|------------|---------|------|-----|----------------------|------------------|
| uid        | integer | 必须   |     | 用户ID                 |                  |
| start_time | integer | 必须   |     | 开始时间，时间戳 |  |
| end_time   | integer | 必须   |     | 结束时间，时间戳               |  |
| ts         | integer | 必须   |     | 时间戳                  |                  |
| nonce      | string  | 必须   |     | 随机字符串                |                  |

## 返回数据

| 名称                     | 类型      | 是否必须 | 默认值 | 备注     | 其他信息             |
|------------------------|---------|------|-----|--------|------------------|
| ret                    | integer | 必须   |     |       |                  |
| msg                    | string  | 必须   |     |       |                  |
| total                  | integer | 非必须 |     |       | 邀请总数          |


### 示例
```json
{
    "ret": 0,
    "msg": "ok",
    "total": 1
}
```