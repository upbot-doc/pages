---
sort: 12
---

# 行为数据上报

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

| 名称                   |      类型      | 是否必须 | 默认值 | 备注                        | 其他信息                                      |
|------------------------|---------------|----------|-------|-----------------------------|----------------------------------------------|
| openid                 |     string    |   必须   |       | 心悦openid                   |                                              |
| game_code              |     string    |   必须   |       | 游戏标识                     |                                              |
| area_id                |     integer   |   必须   |       | 手Q/微信, STD_CHANNEL_DATA   |                                              |
| plat_id                |     integer   |   必须   |       | iOS/Android, STD_SYSTEM_DATA |                                              |
| partition_id           |     integer   |    否    |   0   | 区服id                       |                                              |
| role_name              |     string    |    否    | 空串  | 角色名称                      |                                              |
| mapping_type           |     integer   |   必须   |       | 管理端上传的映射类型, 比如段位  |                                              |
| xinyue_codes           | integer array |   必须   |       | 管理端上传的心悦代号, 比如段位  |                                              |


## 请求示例
```
{
    "openid": "aaa",
    "game_code": "cfm",
    "area_id": 1,
    "plat_id": 2,
    "partition_id": 0,
    "role_name": "bbb",
    "mapping_type": 1,
    "xinyue_codes": [1],
}
```

## 返回数据

|                名称              |           类型         | 是否必须 | 默认值 |       备注      |    其他信息    |
|----------------------------------|-----------------------|----------|-------|-----------------|---------------|
| ret                              |  integer              |   必须   |        |                 |               |
| msg                              |  string               |    否    |  空串  |                 |               |
| data                             |  object               |   必须   |        |     返回数据     |              |
| ├─  xinyue_code_to_is_satisfied  |  map<string, boolean> |   必须   |        |  代号对应是否满足 |              |


## 成功响应
```
{
    "ret": 0,
    "msg": "",
	"data": {
		"xinyue_code_to_is_satisfied": {
			"1": true
		}
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

