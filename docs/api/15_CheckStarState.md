---
sort: 15
---

# 检查用户是否点亮星光

## 接口描述

**Path：** /upbot/api/CheckStarState

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
| openid              |     string    |   必须   |       | 心悦开平openid                                        |                                                         |
| gid              |     array    |   必须   |       | 心悦游戏ID集合，如果集合中某个游戏的星光点亮了就符合                                        |                                                         |

## 请求示例
```
{
    "openid": "xxxxd3dd",
    "gid": 1279
}
```

## 返回数据

|                名称              |           类型         | 是否必须 | 默认值 |       备注                                 |    其他信息     |
|----------------------------------|-----------------------|----------|-------|--------------------------------------------|----------------|
| ret                              |  integer              |   必须   |        |                                           |                |
| msg                              |  string               |    否    |  空串  |                                           |                |
| data                             |  object               |   必须   |        |     返回数据                              |               |
| ├─  ok                        |  bool         |   必须   |        |  是否满足                          |               |


## 成功响应
```
{
    "ret": 0,
    "msg": "",
    "data": {
        "ok": true
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
