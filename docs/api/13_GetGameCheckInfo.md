---
sort: 13
---

# 获取游戏检测信息

## 接口描述

**Path：** /upbot/api/GetGameCheckInfo

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
| game_code              |     string    |   必须   |       | 游戏标识                                        |                                                         |


## 请求示例
```
{
    "game_code": "cfm"
}
```

## 返回数据

|                名称              |           类型         | 是否必须 | 默认值 |       备注                                 |    其他信息     |
|----------------------------------|-----------------------|----------|-------|--------------------------------------------|----------------|
| ret                              |  integer              |   必须   |        |                                           |                |
| msg                              |  string               |    否    |  空串  |                                           |                |
| data                             |  object               |   必须   |        |     返回数据                              |               |
| ├─  items                        |  object array         |   必须   |        |  代号对应是否满足                          |               |
| ├─  ├─ id                        |  integer              |   必须   |        |  游戏数据类型id                            |               |
| ├─  ├─ mapping_type              |  integer              |   必须   |        |  判断的数据类型, 比如段位/声望值             |               |
| ├─  ├─ name                      |  string               |   必须   |        |  判断的数据类型展示的名称, 如第三人称单排段位  |               |
| ├─  ├─ type                      |  integer              |   必须   |        |  检查类型, 1是否/2大小                      |               |
| ├─  ├─ items                     |  object array         |   必须   |        |  判断是否的心悦代号数据                     |               |
| ├─  ├─ ├─ xinyue_code            |  string               |   必须   |        |  心悦代号                                  |               |
| ├─  ├─ ├─ name                   |  string               |   必须   |        |  名称                                      |               |


## 成功响应
```
{
    "ret": 0,
    "msg": "",
    "data": {
        "items": [
            {
                "id": 1,
                "mapping_type": 1,
                "name": "第三人称单排段位",
                "type": 1,
                "items": [
                    {
                        "xinyue_code": "1",
                        "name": "白银"
                    }
                ]
            }
        ]
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

