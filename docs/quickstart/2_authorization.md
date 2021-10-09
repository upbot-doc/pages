---
sort: 2
---

# 开发入门

## 回调地址

为了能够接收推送消息，首先你必须在开发者后台配置回调地址。

当收到相应的触发消息时，开放平台会向该回调地址发送相应的 `HTTP POST` 请求。

每个应用/机器人只能配置一个请求网址，该应用/机器人在所有服务器的消息都会发送到这个地址。

## 接口鉴权

在开发者中心，在创建机器人后，我们可以得到一个 `token`，在请求所有的开放接口时，我们需要在 http header 的 `Authorization` 中加入该 token 以进行鉴权,格式为 `Authorization: TOKEN`。

如下为机器人的鉴权示例:

```
Authorization: 202cb962ac59075b964b07152d234b70
```

## 消息合法性

当有消息发生时，开放平台将会通过 HTTP POST 请求发送 Json 格式的事件数据到你预先提供的回调地址。

在消息中，我们会带上 `verify_token`, 你可以检查 `verify_token` 是否与开发者后台的 `verify_token` 是否 相同以确保这个事件的来源确实是 Bot开放平台，而不是恶意的第三方伪造的事件。

## 功能设置页合法性

机器人可以开发一个 **功能设置** 页面，在每个房间中使用，方便管理机器人在该群的状态及配置等（非必须）。

在打开功能设置页时，url地址会携带 `sig` 字段。

开发者可以使用 `sig` 来校验功能设置页请求的合法性。

`sig` 采用 `JWT` 规范，签名算法为 `HS256`，使用 `token` 做为生成和校验签名的密钥。

playload数据主要包括：

- gid : 房间编号
- bot_id : Bot编号
- uid : 用户编号
- nickname : 用户昵称，默认为房间昵称
- avatar : 用户头像URL，图片无后缀，不影响页面渲染
- iat : 签发时间戳
- exp : 有效期（单位秒）

生成签名示例：
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJnaWQiOjEwMTIzLCJib3RfaWQiOjEwMDAwOTQzNywidWlkIjoxMDAwMDQyNDUsImV4cCI6NzIwMCwiaWF0IjoxNjIzO
TAwNjM0fQ.e3ZrBhQW7zaii-45osUtSGDfQp-85Vma7sZdn2P4HTo
```
