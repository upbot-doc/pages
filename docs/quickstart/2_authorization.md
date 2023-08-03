---
sort: 2
---

# 开发入门

## 接口鉴权

在开发者中心注册应用后，我们可以得到一个 `token`，在请求所有的开放接口时，我们需要在 http header 的 `Authorization` 中加入该 token 以进行鉴权,格式为 `Authorization: TOKEN`。

如下为应用的鉴权示例:

```
Authorization: 202cb962ac59075b964b07152d234b70
```
