---
sort: 12
---

# 检测游戏信息

## 接口描述

**Path：** /upbot/api/CheckGameInfo

**Method：** POST


## 请求参数

### Headers

| 参数名称          | 参数值              | 是否必须 | 示例 | 备注 |
|---------------|------------------|------|----|----|
| Content-Type  | application/json | 是    |    |    |
| Authorization | token            | 是    |    |    |    |

### Body

| 名称                   |      类型      | 是否必须 | 默认值 | 备注                                           | 其他信息                                                 |
|------------------------|---------------|----------|-------|------------------------------------------------|---------------------------------------------------------|
| openid                 |     string    |   必须   |       | 心悦openid                                      |                                                         |
| game_code              |     string    |   必须   |       | 游戏标识                                        |                                                         |
| area_id                |     string    |   必须   |       | 手Q/微信, STD_CHANNEL_DATA                      |                                                         |
| plat_id                |     string    |   必须   |       | iOS/Android, STD_SYSTEM_DATA                    |                                                         |
| partition_id           |     string    |    否    |   0   | 区服id                                          |                                                         |
| role_name              |     string    |    否    | 空串  | 角色名称                                         |                                                         |
| game_check_info_id     |     integer   |   必须   |       | 传入想要判断的数据类型id, 比如cfm的第三人称单排段位 |                                                         |
| xinyue_codes           | string array  |    否    |       | 管理端上传的判断相等的心悦代号, 比如段位           |                                                         |
| compare_info           |     object    |    否    |       | 管理端上传的判断大小的心悦代号, 比如声望值         |                                                         |
| ├─  compare_type       |     integer   |    否    |       | 比较类型, 1相等,2小于,3小于等于,4大于,5大于等于,6区间（左右闭区间）    |                                                         |
| ├─  value              |     integer   |    否    |       | 比较的基准值                                     |                                                         |
| ├─  rvalue              |     integer   |    否    |       | 当compare_type为6时，value表示左区间值，rvalue表示右区间值                                     |            

## 请求示例
```
{
    "openid": "aaa",
    "game_code": "cfm",
    "area_id": "1",
    "plat_id": "2",
    "partition_id": "0",
    "role_name": "bbb",
    "game_check_info_id": 1,
    "xinyue_codes": ["1"]
}
```

## 返回数据

|                名称              |           类型         | 是否必须 | 默认值 |       备注      |    其他信息    |
|----------------------------------|-----------------------|----------|-------|-----------------|---------------|
| ret                              |  integer              |   必须   |        |                 |               |
| msg                              |  string               |    否    |  空串  |                 |               |
| data                             |  object               |   必须   |        |     返回数据     |              |
| ├─  xinyue_code_to_is_satisfied  |  map<string, boolean> |   必须   |        |  代号对应是否满足 |              |
| ├─  compare_is_satisfied         |  boolean              |   必须   |        |  比较是否满足    |              |


## 成功响应
```
{
    "ret": 0,
    "msg": "",
    "data": {
        "xinyue_code_to_is_satisfied": {
            "1": true
        },
        "compare_is_satisfied": false
    }
}
```

## 错误响应
```
{
    "ret": 1001,
    "msg": "请求参数错误，请稍后再试"
}
```

