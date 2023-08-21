---
sort: 1
---

# 查询俱乐部信息

## 接口描述

**Path：** /upbot/api/GetClubBriefInfo

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
| club_id                  | integer    | 必须   |     | 俱乐部ID                    |                                              |
| openid                  | string    | 必须   |     | 游戏家openid                    |                                              |

## 请求示例
```
{
    "club_id": 1223
}
```

## 返回数据

| 名称  | 类型      | 是否必须 | 默认值 | 备注 | 其他信息          |
|-----|---------|------|-----|----|---------------|
| ret | integer | 非必须  |     |    |  |
| msg | string  | 非必须  |     |    |               |
| data | integer  | 非必须  |     |   消息序号 |               |
| ├─ club_id          | integer    | 非必须  |     | 俱乐部ID              |                                              |
| ├─ club_name          | string    | 非必须  |     | 俱乐部名称              |                                              |
| ├─ club_avatar          | string    | 非必须  |     | 俱乐部头像              |                                              |



## 成功响应
```
{
    "ret": 0,
    "msg": "",
    "data": {
        "club_id": 1223,
        "club_name": "王者俱乐部",
        "club_avatar": "https://xdfdfd.dd.jpg"
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

