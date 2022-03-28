---
sort: 3
---

# Bot图片/文字修改信息

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
| signal                                                   | string    | 必须     | 消息类型,1:消息 ,2:心跳;3:加群;4:退群;5:通知修改文本;6:通知修改图片    |
| verify_token                                             | string     | 必须     | 验证token(判断消息合法性)                                        |
| other_info                                               | object[]   | 非必须   | 附加信息                                                        | 
| &nbsp;&nbsp;&nbsp;├ modify_pic_info                      | object[]   | 非必须   | 修改图片信息                 									 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├ uid                | string     | 非必须   | 用户ID, 上报uic的account                                        |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├ currency_id        | string     | 非必须   | 通用ID, 即上报给uic的other数据                                                    |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├ pic_url            | string     | 非必须   | 替换的图片链接, 可以使用该链接替换, 也可以根据自身需求修改                                                     |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├ scene              | integer     | 非必须   | 清除图片场景 1=自定义表情;2=个人头像;3=房间头像 ;4=房间封面;5=gs档案卡头像;6=ns档案卡头像                                         |
| &nbsp;&nbsp;&nbsp;├ modify_text_info                     | object[]    | 非必须   | uic修改文本信息 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├ uid                | string     | 非必须   | 用户ID, 上报uic的account                                        |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├ currency_id        | string     | 非必须   | 通用ID, 即上报给uic的other数据                                                    |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├ text               | string     | 非必须   | 替换文本, 可以使用该文本替换, 也可以根据自身需求修改改                                                     |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├ scene              | integer     | 非必须   | 修改用户文本 14=抽奖信息;24=投票                                       |

##### 示例

```json
{
	"signal": 5,
	"verify_token": "verify_token",
	"other_info": {
		"modify_text_info": {
			"uid": "100002628",
			"currency_id": "16425-14280",
			"text": "替换内容",
			"scene":24
		}
	}
}
```
