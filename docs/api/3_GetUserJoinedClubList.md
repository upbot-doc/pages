---
sort: 3
---

# 查询用户加入的俱乐部信息（包括职位信息）

## 接口描述

**Path：** /upbot/api/GetUserJoinedClubList

**Method：** POST


## 请求参数

### Headers

| 参数名称          | 参数值              | 是否必须 | 示例 | 备注 |
|---------------|------------------|------|----|----|
| Content-Type  | application/json | 是    |    |    |
| Authorization | token            | 是    |    |    |

### Body

| 名称                   | 类型         | 是否必须 | 默认值 | 备注                        | 其他信息                                         |
|----------------------|------------|------|-----|---------------------------|----------------------------------------------|
| openid                  | string    | 必须   |     | 心悦openid                    |                                              |


## 请求示例
```
{
    "openid": "JHhd993hGG8n0dsfn9hhsdhfi"
}
```

## 返回数据

| 名称  | 类型      | 是否必须 | 默认值 | 备注 | 其他信息          |
|-----|---------|------|-----|----|---------------|
| ret | integer | 非必须  |     |    |  |
| msg | string  | 非必须  |     |    |               |
| data | Array  | 非必须  |     |   数组 |               |
| ├─ club_info | object  | 非必须  |     |   数组 |               |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─ club_id          | integer    | 非必须  |     | 俱乐部ID              |                                              |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─ club_name        | string    | 非必须  |     | 俱乐部名称              |                                              |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─ club_avatar      | string    | 非必须  |     | 俱乐部头像              |                                              |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─ gid          | integer    | 非必须  |     | 俱乐部游戏id              |                                              |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─ game_code        | string    | 非必须  |     | 俱乐部游戏code              |                                              |
| &nbsp;&nbsp;&nbsp;&nbsp; ├─ club_level_v2        | object    | 非必须  |     | 俱乐部等级信息              |                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ├─ club_level_point        | object    | 非必须  |     | 俱乐部等级信息              |                                              |                
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ├─ level        | integer    | 非必须  |     | 俱乐部等级              |                                              |                
| ├─ role_name          | string    | 非必须  |     | 职位名称              |                                              |
| ├─ join_time          | integer    | 非必须  |     | 最近一次加入时间              |                                              |

## 成功响应
```
{
    "ret": 0,
    "msg": "",
    "data": [{
        "club_info":{
            "club_id":258,
            "club_name":"苏苏宝贝",
            "club_avatar":"https://333454xxx.jpg",
            "gid": 123,
            "game_code": "xddd",
            "club_level_v2": {
                "club_level_point": {
                    "level": 10
                }
            }
        },
        "role_name": "创建者",
        "join_time": 123343434
    }]
}
```

## 错误响应
```
{
	"ret": 1001,
	"msg": "请求参数错误，请稍后再试"
}
``` 

