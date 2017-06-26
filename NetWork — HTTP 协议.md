# HTTP 协议
### HTTP 基本概念
- #### 超文本传输协议(Hypertext Transfer Protocol，简称HTTP)，与 FTP 、Telnet、SMTP 等协议一样，是应用层协议。

- ####

- #### 1997年1月，HTTP/1.1 版本发布，相比 1.0 版本它进一步完善了 HTTP 协议，直到现在还是最流行的版本。

- #### HTTP/1.1 版本最大的变化，就是引入了持久连接（persistent connection），即 TCP 连接默认不关闭，可以被多个请求复用，不需要明确声明 Connection: keep-alive。客户端和服务器发现对方一段时间没有活动，都可以主动关闭连接。不过，规范的做法是，客户端在最后一个请求时，发送Connection: close，明确要求服务器关闭TCP连接。

### HTTP 请求报文
#### 1. 请求方法 URI 协议/版本
#### 类似于 xhr.open(method, url, isAsync)

#### 2. 请求头(Request Header)
#### 3. 请求正文
#### 4. 请求正文


### HTTP 响应报文



### HTTP 请求方法
- #### PUT（增）
- #### DELETE（删）
- #### POST（改）
- #### GET（查）
- #### HEAD
- #### OPTIONS
- #### TRACE
- #### CONNECT
