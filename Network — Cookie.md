## Cookie
> HTTP 协议是无状态的，它只负责通信，不保存数据。要保存状态（数据）传统的方式是 cookie 或 session。


---
##### Cookie 是 HTTP 协议中的一个请求首部

- 服务器端的 Cookie 信息是通过 HTTP 的 Set-Cookie 首部来投放并存储到客户端的。

- 客户端的 Cookie 是通过 HTTP 的 Cookie 首部返回给服务器端的。

- Cookie 分为 会话cookie（生命周期和浏览器同步，与 sessionStorage 不同） 和 永久cookie（设置 expire 属性）。

- 如图展示了 Cookie 与 HTTP 的关系

  ![Cookie与Http](https://github.com/StRothschild/Network/blob/master/resource/NetWork%20%E2%80%94%20Cookie.png?raw=true)





---
#### Cookie 参数
- expires: 过期时间，格式为GMT时间，这个时间以客户端时间为标准。

- max-age: 有效期，单位为秒，这个时间以文档第一次被请求时服务器记录的Request_time为标准。

- 不设置 max-age 和 expire 的情况下 Cookie 会在浏览器关闭时自动删除，称为会话 Cookie，值被存储在内存中。设置了 max-age 或 expire 时候，称为持久性 Cookie，值被存储在磁盘中。

- httpOnly: 默认为true, 此时cookie不能通过 document.cookie 获取
