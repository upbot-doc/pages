---
sort: 2
---

# 查询游戏家所在的俱乐部职位信息

## 接口描述

**Path：** /upbot/api/GetPlayerClubRole

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
| ├─ club_id          | integer    | 非必须  |     | 俱乐部ID              |                                              |
| ├─ name          | string    | 非必须  |     | 俱乐部名称              |                                              |
| ├─ is_creator          | bool    | 非必须  |     | 是否是创建者              |                                              |
| ├─ role_name          | string    | 非必须  |     | 职位名称              |                                              |


## 成功响应
```
{
    "ret": 0,
    "msg": "",
    "data": [{
        "club_id": 1223,
        "name": "王者俱乐部",
        "is_creator": true,
        "role_name": "创建者",
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

