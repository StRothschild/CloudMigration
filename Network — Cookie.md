## Cookie
> HTTP 协议是无状态的，它只负责通信，不保存数据。要保存状态（数据）传统的方式是 cookie 或 session。

##### Cookie 是 HTTP 协议中的一个请求首部。
##### 服务器端的 Cookie 信息是通过 HTTP 的 Set-Cookie 首部来投放并存储到客户端的。
##### 客户端的 Cookie 是通过 HTTP 的 Cookie 首部返回给服务器端的。
##### Cookie 分为 会话cookie（生命周期和浏览器同步，与 sessionStorage 不同） 和 永久cookie（设置 expire 属性）。
