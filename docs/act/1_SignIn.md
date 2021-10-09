---
sort: 1
---

# 房间签到

## 基本信息

**Path：** /api/act/SignIn

**Method：** POST

**接口描述：**

## 请求参数

### Headers

| 参数名称          | 参数值              | 是否必须 | 示例 | 备注 |
|---------------|------------------|------|----|----|
| Content-Type  | application/json | 是    |    |    |
| Authorization | token            | 是    |    |    |

### Body

| 名称         | 类型      | 是否必须 | 默认值 | 备注                   | 其他信息                         |
|------------|---------|------|-----|----------------------|------------------------------|
| serial_id  | string  | 必须   |     | 流水id，不可重复            | 开发者自己生成                      |
| gid        | integer | 必须   |     | 房间ID                 |                              |
| act_id     | integer | 必须   | 0   | 活动ID，用于区分多期开放的签到活动   |                              |
| start_date | string  | 必须   |     | 活动开始日期，用于区分多期开放的签到活动 | date格式均为20060102             |
| end_date   | string  | 非必须  |     | 活动结束日期               | date格式均为20060102             |
| cycle      | integer | 非必须  |     | 签到周期，单位：天            |                              |
| sign_type  | integer | 必须   | 0   | 签到活动类型，必填2           | 0连续签到，1非连续签到，2连续签到并且需要查询统计信息 |
| uid        | integer | 必须   |     | 用户ID                 |                              |
| sign_date  | string  | 必须   |     | 签到日期                 | date格式均为20060102             |
| ts         | integer | 必须   |     | 时间戳                  |                              |
| nonce      | string  | 必须   |     | 随机字符串                |                              |

#### 补充说明
签到时，使用 `gid`, `act_id`, `start_date` [,end_date,cycle] 做为一次签到活动的唯一标识，`end_date`,`cycle` 非必填。

查询时，需要传签到时的上述参数。

## 返回数据

| 名称  | 类型      | 是否必须 | 默认值 | 备注                   | 其他信息 |
|-----|---------|------|-----|----------------------|------|
| ret | integer | 必须   | 0   |                      |      |
| msg | string  | 必须   | ok  |                      |      |
