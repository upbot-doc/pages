---
sort: 4
---

# 判断用户是否有权限

## 基本信息

**Path：** /api/v1/CheckUserHasPerm

**Method：** POST

**接口描述：**


## 请求参数
**Headers**

| 参数名称          | 参数值              | 是否必须 | 示例 | 备注 |
|---------------|------------------|------|----|----|
| Content-Type  | application/json | 是    |    |    |
| Authorization | token            | 是    |    |    |

**Body**

| 名称       | 类型      | 是否必须 | 默认值 | 备注   | 其他信息 |
|----------|---------|------|-----|------|------|
| gid      | integer | 必须   |     | 群组ID |      |
| uid      | integer | 必须   |     | 用户ID |      |
| perms_id | integer | 必须   |     | 权限ID |      |

## 返回数据

| 名称  | 类型      | 是否必须 | 默认值 | 备注                   | 其他信息 |
|-----|---------|------|-----|----------------------|------|
| ret | integer | 必须   | 0   |                      |      |
| msg | string  | 必须   | ok  |                      |      |
| has | bool    | 必须   |     | true-有权限 false-无权限 |      |