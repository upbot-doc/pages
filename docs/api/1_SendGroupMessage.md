---
sort: 1
---

# 发送群消息

## 基本信息

**Path：** /api/v1/SendGroupMessage

**Method：** POST

**接口描述：**

## 请求参数

### Headers

| 参数名称          | 参数值              | 是否必须 | 示例 | 备注 |
|---------------|------------------|------|----|----|
| Content-Type  | application/json | 是    |    |    |
| Authorization | token            | 是    |    |    |

### Body

| 名称                   | 类型         | 是否必须 | 默认值 | 备注                        | 其他信息                                         |
|----------------------|------------|------|-----|---------------------------|----------------------------------------------|
| gid                  | integer    | 必须   |     | 目标群组ID                    |                                              |
| target_id            | string     | 必须   |     | 目标频道ID                    |                                              |
| l2_type              | integer    | 必须   | 0   | 消息内容类型                    | 枚举: 1文本；2视频；3图片；8markdown；12混合消息             |
| l3_types             | integer [] | 非必须  |     | 消息包含类型                    | []，枚举：1回复；2表态；3@消息 4链接                       |
| ts                   | integer    | 必须   |     | 时间戳                       |                                              |
| nonce                | string     | 必须   |     | 随机字符串                     |                                              |
| body                 | object     | 非必须  |     | 消息内容                      |                                              |
| ├─ content           | string     | 非必须  |     | 文本；markdown               |                                              |
| ├─ video_info        | object []  | 非必须  |     | 视频消息                      | [{},{}]                                      |
| ├─ pic_info          | object []  | 非必须  |     | 图片消息                      | [{},{}]                                      |
| ├─ reply_msg         | object     | 非必须  |     | 回复消息                      | {}                                           |
| ├─ at_msg            | object     | 非必须  |     | @消息 at消息                  | {}                                           |
| ├─ link_to_msg       | object []  | 非必须  |     | 链接跳转消息                    | [{},{}]                                      |
| ├─ mixed_msg         | object     | 非必须  |     | 混合消息排序控制                  | 文本、图片、视频 排序                                  |
| ├─ bot_data          | object     | 非必须  |     | Bot特殊消息                   |                                              |


### 文本消息

| 名称                   | 类型         | 是否必须 | 默认值 | 备注                        | 其他信息                                         |
|----------------------|------------|------|-----|---------------------------|----------------------------------------------|
| content           | string     | 非必须  |     | 文本；markdown               |      l2_type=1 或者 l2_type=8                                         |

#### 示例

```
{
	"l2_type": 1,
	"body": {
		"content": "文本消息"
	}
}
```

### 视频消息

| 名称                   | 类型         | 是否必须 | 默认值 | 备注                        | 其他信息                                         |
|----------------------|------------|------|-----|---------------------------|----------------------------------------------|
| video_info        | object []  | 非必须  |     | 视频消息                      | [{},{}]                                      |
| ├─ video_url       | string     | 非必须  |     | 视频地址                      |                                              |
| ├─ video_size      | integer    | 非必须  |     | 视频数据大小，单位：字节              |                                              |
| ├─ video_second    | integer    | 非必须  |     | 视频时长，单位：秒                 |                                              |
| ├─ video_format    | string     | 非必须  |     | 视频格式，例如 mp4               |                                              |
| ├─ thumb_url       | string     | 非必须  |     | 视频缩略图地址                   |                                              |
| ├─ thumb_size      | integer    | 非必须  |     | 缩略图大小，单位：字节               |                                              |
| ├─ thumb_width     | integer    | 非必须  |     | 缩略图宽度                     |                                              |
| ├─ thumb_height    | integer    | 非必须  |     | 缩略图高度                     |                                              |
| ├─ thumb_format    | string     | 非必须  |     | 缩略图格式，例如 JPG、BMP 等        |                                              |
| ├─ video_width     | integer    | 非必须  |     | 视频宽度                      |                                              |
| ├─ video_height    | integer    | 非必须  |     | 视频高度                      |                                              |

#### 示例

```
{
	"l2_type": 2,
	"body": {
		"video_info": [{
			"video_url": "video.mp4",
			"video_size": 54100,
			"video_second": 36,
			"video_format": "mp4",
			"thumb_url": "https://www.example.com/image.jpg",
			"thumb_width": 80,
			"thumb_height": 60,
			"thumb_format": "JPG",
			"video_width": 400,
			"video_height": 100
		}, {
			"video_url": "video.mp4",
			"video_size": 54100,
			"video_second": 36,
			"video_format": "mp4",
			"thumb_url": "https://www.example.com/image.jpg",
			"thumb_width": 80,
			"thumb_height": 60,
			"thumb_format": "JPG",
			"video_width": 400,
			"video_height": 100
		}]
	}
}
```

### 图片消息

| 名称                   | 类型         | 是否必须 | 默认值 | 备注                        | 其他信息                                         |
|----------------------|------------|------|-----|---------------------------|----------------------------------------------|
| pic_info          | object []  | 非必须  |     | 图片消息                      | [{},{}]                                      |
| ├─ uuid            | string     | 非必须  |     | 图片序列号。后台用于索引图片的键值。        |                                              |
| ├─ image_format    | integer    | 非必须  | 0   | 图片格式                      | 枚举: JPG = 1，GIF = 2，PNG = 3，BMP = 4，其他 = 255 |
| ├─ image_info_array | object []  | 非必须  |     | 图片具体信息                    | [{},{}]                              |
| ├─── type       | integer    | 非必须  |     | 图片类型                      | 1-原图，2-缩略图                                   |
| ├─── size        | integer    | 非必须  |     | 图片数据大小，单位：字节              |                                              |
| ├─── width       | integer    | 非必须  |     | 图片宽度                      |                                              |
| ├─── height      | integer    | 非必须  |     | 图片高度                      |                                              |
| ├─── url         | string     | 非必须  |     | 图片地址                      |                                              |
| ├───md5sum      | string     | 非必须  |     | 图片md5                     |                                              |

#### 示例

```
{
	"l2_type": 3,
	"body": {
		"pic_info": [{
				"uuid": "abc3788c-cf7c-447c-baae-30f38249ccc5",
				"image_format": 1,
				"image_info_array": [{
					"url": "https://www.example.com/image.jpg",
					"type": 1,
					"size": 4301,
					"width": 400,
					"height": 300,
					"md5sum": "03c7c0ace395d80182db07ae2c30f034"
				}]
			},
			{
				"uuid": "abc3788c-cf7c-447c-baae-30f38249ccc5",
				"image_format": 1,
				"image_info_array": [{
					"url": "https://www.example.com/image.jpg",
					"type": 2,
					"size": 4301,
					"width": 400,
					"height": 300,
					"md5sum": "03c7c0ace395d80182db07ae2c30f034"
				}]
			}
		]
	}
}
```

### 回复消息

| 名称                   | 类型         | 是否必须 | 默认值 | 备注                        | 其他信息                                         |
|----------------------|------------|------|-----|---------------------------|----------------------------------------------|
| reply_msg         | object     | 非必须  |     | 回复消息                      | {}                                           |
| ├─ uid_replied     | integer    | 非必须  |     | 被回复者uid                   |                                              |
| ├─ content         | string     | 非必须  |     | 被回复的消息内容,展示用              |                                              |
| ├─ msg_seq         | integer    | 非必须  |     | 被回复的消息唯一标识                |                                              |
| ├─ msg_id          | string     | 非必须  |     | 消息id                      |                                              |

#### 示例

```
{
	"l3_types": [1],
	"body": {
		"reply_msg": {
			"content": "[图片]",
			"uid_replied": "10000086",
			"msg_seq": "200002121210000086",
			"msg_id": "03c7c0ace395d80182db07ae2c30f034"
		}
	}
}
```

### @消息

| 名称           | 类型       | 是否必须 | 默认值 | 备注                                 | 其他信息          |
| -------------- | ---------- | -------- | ------ | ------------------------------------ | ----------------- |
| at_msg         | object     | 非必须   |        | @消息 at消息                         | {}                |
| ├─ at_type     | integer    | 非必须   | 0      | @类型,部分@时候才需要填写at_uid_list | 1-部分人 2-所有人 |
| ├─ at_uid_list | integer [] | 非必须   |        | 被@用户id列表                        |                   |

#### 示例

```
{
	"l3_types": [3],
	"body": {
		"at_msg": {
			"at_type": 1,
			"at_uid_list": [10000086, 100000032]
		}
	}
}
```


### 链接消息

| 名称              | 类型        | 是否必须 | 默认值 | 备注                   | 其他信息               |
|-----------------|-----------|------|-----|----------------------|--------------------|
| link_to_msg     | object [] | 非必须  |     | 链接跳转消息               | [{},{}]            |
| ├─ type         | integer   | 非必须  | 0   | 链接类型                 | 1-频道；2-外站；3-Bot设置页 |
| ├─ display_name | string    | 非必须  |     | 显示文案                 |                    |
| ├─ channel_ext  | object    | 非必须  |     | 频道跳转内容 type=1        | {}                 |
| ├─── gid        | integer   | 非必须  |     | 群组ID                 | 仅支持相同群组频道跳转        |
| ├─── cid        | string    | 非必须  |     | 频道ID                 |                    |
| ├─ website_ext  | object    | 非必须  |     | 外站跳转内容 type=2        | {}                 |
| ├─── url        | string    | 非必须  |     | 链接地址                 | 必须 https           |
| ├─ botconf_ext  | object    | 非必须  |     | Bot设置页 type=3        | {}                 |
| ├─── gid        | integer   | 非必须  |     | 群组ID                 | 仅支持相同群组Bot配置页跳转    |
| ├─── bot_id     | integer   | 非必须  |     | Bot ID               |                    |
| ├─ h5_ext       | object    | 非必须  |     | H5带sig参数 type=5      | {}                 |
| ├─── gid        | integer   | 非必须  |     | 群组ID                 | 仅支持相同群组Bot配置页跳转    |
| ├─── bot_id     | integer   | 非必须  |     | Bot ID               |                    |
| ├─── url        | string    | 非必须  |     | H5链接地址               | 必须 https           |
| ├─botcustom_ext | object    | 非必须  |     | 带自定义参数扽Bot设置页 type=6 | {}                 |
| ├─── gid        | integer   | 非必须  |     | 群组ID                 |                    |
| ├─── bot_id     | integer   | 非必须  |     | Bot ID               |                    |
| ├─── params     | string    | 非必须  |     | 自定义参数，必须为json格式字符串   | 会透传到配置页            |


#### 示例

```
{
	"l3_types": [4],
	"body": {
		"link_to_msg": [{
			"type": 3,
			"displayName": " 配置跳转 ",
			"botconf_ext": {
				"gid": 10086,
				"bot_id": 100000001
			}
		}, {
			"type": 1,
			"displayName": "频道跳转 ",
			"channel_ext": {
				"gid": 10086,
				"cid": "10088"

			}
		}, {
			"type": 2,
			"displayName": "外站跳转 ",
			"website_ext": {
				"url": "https://www.example.com/"
			}
		}, {
			"type": 5,
			"displayName": "H5",
			"h5_ext": {
				"gid": 10123,
				"bot_id": 100000030,
				"url": "https://www.example.com/"
			}
		}, {
			"type": 6,
			"displayName": "自定义bot配置页",
			"botcustom_ext": {
				"gid": 10123,
				"bot_id": 100000030,
				"params": "{\"gid\":15407,\"botId\":\"100000007\"}"
			}
		}]
	}
}
```

### 混合消息

| 名称                   | 类型         | 是否必须 | 默认值 | 备注                        | 其他信息                                         |
|----------------------|------------|------|-----|---------------------------|----------------------------------------------|
| mixed_msg         | object     | 非必须  |     | 混合消息排序控制                  | 文本、图片、视频 排序                                  |
| ├─ msg_item_list   | object []  | 非必须  |     | 排序规则                      | [{"l2_type":1},{"l2_type":2}]                |
| ├─── l2_type       | integer    | 非必须  |     | 待排序的消息类型                  |                                              |


#### 示例

```
{
	"l2_type": 12,
	"body": {
		"content": "文本+图片混合消息",
		"pic_info": [{
			"uuid": "abc3788c-cf7c-447c-baae-30f38249ccc5",
			"image_format": 1,
			"image_info_array": [{
				"url": "https://www.example.com/image.jpg",
				"type": 2,
				"size": 4301,
				"width": 400,
				"height": 300,
				"md5sum": "03c7c0ace395d80182db07ae2c30f034"
			}]
		}],
		"mixed_msg": {
			"msg_item_list": [{
					"l2_type": 3
				},
				{
					"l2_type": 1
				}
			]
		}
	}

}
```

### 机器人消息

| 名称                   | 类型         | 是否必须 | 默认值 | 备注                        | 其他信息                                         |
|----------------------|------------|------|-----|---------------------------|----------------------------------------------|
| bot_data          | object     | 非必须  |     | Bot特殊消息                   |                                              |
| ├─ cmd_id          | integer    | 非必须  |     | Bot消息命中的指令ID              |                                              |

#### 示例

```
"body":{
    "bot_data":{
        "cmd_id":10000086
    }
}
```


## 返回数据

| 名称  | 类型      | 是否必须 | 默认值 | 备注 | 其他信息          |
|-----|---------|------|-----|----|---------------|
| ret | integer | 非必须  |     |    |  |
| msg | string  | 非必须  |     |    |               |


## 请求示例

```
{
    "gid": "10123",
    "target_id": "10802",
    "ts": 1234567890,
    "nonce": "123",
    "l2_type": 12,
    "body": {
        "content": "示例混合消息文本+视频",
        "video_info": [
            {
                "video_url": "https://www.example.com/video.mp4",
                "video_size": 54100,
                "video_second": 36,
                "video_second": "mp4",
                "thumb_url": "https://www.example.com/image.jpg",
                "thumb_width": 80,
                "thumb_height": 60,
                "thumb_format": "JPG",
                "video_width": 400,
                "video_height": 100
            }
        ],
        "at_msg": {
            "at_type": 1,
            "at_uid_list": [
                100004245
            ]
        },
        "mixed_msg": {
            "msg_item_list": [
                {
                    "l2_type": 1
                },
                {
                    "l2_type": 2
                }
            ]
        }
    }
}

```
