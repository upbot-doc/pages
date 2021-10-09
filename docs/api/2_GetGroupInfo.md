---
sort: 2
---

# 获取房间信息

## 基本信息

**Path：** /api/v1/GetGroupInfo

**Method：** POST

**接口描述：**


## 请求参数
**Headers**

| 参数名称          | 参数值              | 是否必须 | 示例 | 备注 |
|---------------|------------------|------|----|----|
| Content-Type  | application/json | 是    |    |    |
| Authorization | token            | 是    |    |    |

**Body**

| 名称  | 类型      | 是否必须 | 默认值 | 备注   | 其他信息 |
|-----|---------|------|-----|------|------|
| gid | integer | 必须   |     | 房间ID |      |

## 返回数据

| 名称            | 类型      | 是否必须 | 默认值 | 备注     | 其他信息      |
|---------------|---------|------|-----|--------|-----------|
| ret           | integer | 必须   |     |        |           |
| ret           | integer | 必须   |     |        |           |
| msg           | string  | 必须   |     |        |           |
| group_info    | object  | 非必须  |     |        | {}        |
| group_info    | object  | 非必须  |     |        | {}        |
| ├─ gid        | string  | 非必须  |     | 房间ID   |           |
| ├─ avatar     | string  | 非必须  |     | 房间头像   |           |
| ├─ name       | string  | 非必须  |     | 房间名称   |           |
| ├─ profile    | string  | 非必须  |     | 简介     |           |
| ├─ def_cid    | string  | 非必须  |     | 默认频道ID |           |
| ├─ creator_id | string  | 非必须  |     | 房间创建者ID |           |
| ├─ create_uts | string  | 非必须  |     | 创建时间戳秒  |           |
| ├─ status     | integer | 非必须  | 1   | 状态     | 1 有效 2 删除 |
| ├─ deleter_id | string  | 非必须  | "0" | 删除者ID |           |
| ├─ del_uts    | string  | 非必须  | "0" | 删除时间戳秒  |           |
| ├─ cate_list    | object []  | 非必须  |  | 房间频道分类列表  |[{},{}]           |
| ├─── caid    | string  | 非必须  |  |  分类ID |         |
| ├─── name    | string  | 非必须  |  | 分类名称  |        |