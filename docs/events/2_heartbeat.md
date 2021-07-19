---
sort: 2
---

# Bot心跳消息

## 基本信息

**Path：** /{第三方提供的接收地址}

**Method：** POST

**接口描述：**


## 消息参数

### Headers

| 参数名称      | 参数值           | 是否必须 | 示例 | 备注 |      |
| ------------- | ---------------- | -------- | ---- | ---- | ---- |
| Content-Type  | application/json | 是       |      |      |      |

### Body

| 名称                                                      | 类型       | 是否必须 | 备注                                                         |
| ------------                                             | ---------- | -------- | :----------------------------------------------------------- |
| signal                                                   | integer    | 必须     | 消息类型 2:心跳                        |
| verify_token                                             | string     | 必须     | 验证token(判断消息合法性)                                   |
| heartbeat                                                | string     | 必须     | 消息类型为2时，需原样返回                                  |

##### 示例

```json
{
	"signal": 2,
	"verify_token": "verify_token",
	"heartbeat": "heartbeat"
}
```



### 响应

| 名称  | 类型      | 备注              |
|-----|---------|-----------------|
| ret | integer | 返回码,0:成功 非0:错误码 |
| msg | string  | 结果              |
| heartbeat | string  | 原样返回字符串              |

##### 示例

```json
{
	"ret": 0,
	"msg": "ok",
	"heartbeat": "heartbeat"
}
```
