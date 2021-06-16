---
sort: 3
---

# 获取群组频道列表

### 基本信息

**Path：** /api/v1/GetGroupChannelList

**Method：** POST

**接口描述：**


### 请求参数
**Headers**

| 参数名称          | 参数值              | 是否必须 | 示例 | 备注 |
|---------------|------------------|------|----|----|
| Content-Type  | application/json | 是    |    |    |
| Authorization | token            | 是    |    |    |

**Body**

| 名称  | 类型      | 是否必须 | 默认值 | 备注 | 其他信息 |
|-----|---------|------|-----|----|------|
| gid | integer | 必须   |     |    |      |



### 返回数据

| 名称             | 类型        | 是否必须 | 默认值 | 备注                           |
|----------------|-----------|------|-----|------------------------------|
| ret            | integer   | 非必须  |     |                              |
| msg            | string    | 非必须  |     |                              |
| channel_list   | object [] | 非必须  |     | 频道列表                         |
| ├─ cid         | string    | 非必须  |     | 频道ID                         |
| ├─ name        | string    | 非必须  |     | 频道名称                         |
| ├─ profile     | string    | 非必须  |     | 简介                           |
| ├─ caid        | string    | 非必须  |     | 归属分类ID                       |
| ├─ gid         | string    | 非必须  |     | 归属群组ID                       |
| ├─ is_cmd_chan | integer   | 非必须  |     | 0 普通频道 1 低优先级信令频道 2 高优先级信令频道 |
| ├─ cid_str     | string    | 非必须  |     | str类型频道ID                    |
| ├─ mem_num     | integer   | 非必须  |     | 频道成员数                        |
| ├─ score       | string    | 非必须  |     | 创建初始分值                       |
| ├─ block       | integer   | 非必须  |     | 禁言                           |
| ├─ status      | integer   | 非必须  |     | 状态                           |
| ├─ creator_id  | string    | 非必须  |     | 创建用户ID                       |
| ├─ crt_uts     | string    | 非必须  |     | 创建时间戳秒                       |
| ├─ deleter_id  | string    | 非必须  |     | 删除者ID                        |
| ├─ del_uts     | string    | 非必须  |     | 删除时间戳秒                       |
