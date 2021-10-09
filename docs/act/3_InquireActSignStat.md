---
sort: 3
---

# 查询整个活动签到的统计信息

## 基本信息

**Path：** /api/act/InquireActSignStat

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
| gid        | integer | 必须   |     | 房间ID                 |                  |
| act_id     | integer | 必须   | 0   | 活动ID，用于区分多期开放的签到活动   |                  |
| start_date | string  | 必须   |     | 活动开始日期，用于区分多期开放的签到活动 | date格式均为20060102 |
| end_date   | string  | 非必须  |     | 活动结束日期               | date格式均为20060102 |
| cycle      | integer | 非必须  |     | 签到周期，单位：天            |                  |
| offset     | integer | 非必须  | 0   | 分页偏移                 |                  |
| limit      | integer | 必须   |     | 返回结果上限               |                  |
| order_by   | string  | 非必须  |     | 排序方式                 |                  |
| ts         | integer | 必须   |     | 时间戳                  |                  |
| nonce      | string  | 必须   |     | 随机字符串                |                  |

#### 分页说明
offset、limit表示查询偏移位置和返回结果上限（同时适用于分页和滚动加载，分页时根据页码和每页数量计算offset即可）

#### 排序说明
order_by表示排序方式，支持字段: total_signed、continuous_signed、has_signed_today，格式： `[+/-][字段](,)……` 
例如：按总签到数升序：`+total_signed`，按总签到数降序：`-total_signed`；
**暂不支持组合顺序**：先按总签到数升序，再按连续签到降序：`+total_signed,-continuous_signed`

## 返回数据

| 名称                     | 类型      | 是否必须 | 默认值 | 备注     | 其他信息             |
|------------------------|---------|------|-----|--------|------------------|
| ret                    | integer | 必须   |     |        |                  |
| msg                    | string  | 必须   |     |        |                  |
| data                   | object  | 非必须  |     |        | {}               |
| ├─ total               | integer | 非必须  |     | 累计签到次数 |                  |
| ├─ payload             | integer | 非必须  |     | 连续签到次数 | [{},{},{}]       |
| ├─── uid               | string  | 非必须  |     | 用户ID   |                  |
| ├─── total_signed      | string  | 非必须  |     | 累计签到次数 | "0"              |
| ├─── continuous_signed | string  | 非必须  |     | 连续签到次数 | "0"              |
| ├─── has_signed_today  | bool    | 非必须  |     | 今天是否已签 | true：已签，false：未签 |
| ├─── latest_sign_date  | string  | 非必须  |     | 最近签到日期 | date格式均为20060102 |

### 示例
```json
{
    "ret": 0,
    "msg": "ok",
    "data": {
        "total": 1,
        "payload": [
            {
                "uid": "100000086",
                "total_signed": "2",
                "continuous_signed": "0",
                "has_signed_today": false,
                "latest_sign_date": "20211006"
            }
        ]
    }
}
```