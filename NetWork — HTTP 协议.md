# HTTP 协议
### HTTP 基本概念
- #### 超文本传输协议(Hypertext Transfer Protocol，简称HTTP)，与 FTP 、Telnet、SMTP 等协议一样，是应用层协议。

- #### 1997年1月，HTTP/1.1 版本发布，相比 1.0 版本它进一步完善了 HTTP 协议，直到现在还是最流行的版本。

- #### HTTP/1.1 版本最大的变化，就是引入了持久连接（persistent connection），即 TCP 连接默认不关闭，可以被多个请求复用，不需要明确声明 Connection: keep-alive。客户端和服务器发现对方一段时间没有活动，都可以主动关闭连接。不过，规范的做法是，客户端在最后一个请求时，发送Connection: close，明确要求服务器关闭TCP连接。



---
### HTTP 请求报文
![请求报文结构](https://github.com/StRothschild/NetWork/blob/master/resource/NetWork%20%E2%80%94%20HTTP%20%E8%AF%B7%E6%B1%82%E4%BD%93%E7%BB%93%E6%9E%84.jpg?raw=true)

#### 1. 请求行
  - #### 方法 URI 协议/版本（GET https://github.com:80/ HTTP/1.1）
  - #### 十分类似于 XMLHttpRequest 中的 xhr.open(method, url, isAsync)

#### 2. 请求首部(Request Header)
  - ##### Host：www.baidu.com
  - ##### User-Agent：Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.7.6)
  - ##### Accept：text/plain, text/html
  - ##### Accept-Charset：utf-8
  - ##### Date：浏览器消息发出的时间
  - ##### Content-Type： application/x-www-form-urlencoded
  - ##### Content-Length：请求消息正文的长度
  - ##### Cache-Control：no-cache
  - ##### Connection：close
  - ##### Cookie：HTTP 请求发送时，会把保存在该请求域名下的所有cookie值一起发送给 web 服务器。


#### 3. 空行
  ##### 即使第四部分的请求数据为空，也必须有空行。

#### 4. 请求体(Request body)
  ##### 请求数据，可以为空


---
### HTTP 响应报文
![响应报文结构](https://github.com/StRothschild/NetWork/blob/master/resource/NetWork%20%E2%80%94%20HTTP%20%E5%93%8D%E5%BA%94%E4%BD%93%E7%BB%93%E6%9E%84.png?raw=true)

#### 1. 响应行
  - #### 协议/版本 状态码 状态信息（HTTP/1.1 200 OK）

#### 2. 响应首部(Response Header)
  - ##### Content-Type：text/html
  - ##### Content-Length：响应体的长度
  - ##### Cache-Control：no-cache
  - ##### Date：原始服务器消息发出的时间
  - ##### Expires：响应过期的日期和时间
  - ##### Last-Modified：请求资源的最后修改时间


#### 3. 空行
  ##### 即使第四部分的请求数据为空，也必须有空行。

#### 4. 响应体(Response body)
  ##### 返回的数据，可以为空






---
### HTTP 请求方法
- #### PUT（增）
- #### DELETE（删）
- #### POST（改）
- #### GET（查）
- #### HEAD
  ##### HEAD 与 GET 十分相似，只不过 HEAD 请求只返回响应头，而不会发送响应内容。当我们只需要查看某个页面的状态的时候，使用 HEAD 是非常高效的，因为在传输的过程中省去了页面内容。
- #### OPTIONS
- #### TRACE
- #### CONNECT

- #### PATCH
- #### COPY
- #### MOVE
- #### LINK
- #### UNLINk
- #### WRAPPED
- #### Extension-mothed






---
### GET 与 POST 的区别
- #### 通过 GET 提交的数据必须放在 URL 中；而通过 POST 提交的数据放在请求体中。
- #### GET 方式提交的数据最多只能是 1024 字节；而 POST 理论上没有限制，可传较大量的数据。
- #### 通过 GET 提交数据，信息明文出现在 URL 上，所以有可能通过浏览器的页面缓存，或是历史纪录造成数据泄露。除此之外，使用GET提交数据还可能会造成 Cross-site request forgery 攻击。
- #### GET 和 POST 都是明文传输，可能被抓包，所以都不安全。想要安全最好进行加密传输，就是用 HTTPS。





---
### HTTP 状态码（status）
#### status 状态码由三位数字组成，第一位数字表示响应的类型，常用的状态码有五大类如下所示：

- #### 1xx：信息，服务器收到请求，需要请求者继续执行操作;

- #### 2xx：成功，操作被成功接收并处理;

- #### 3xx：重定向，需要进一步的操作以完成请求;

- #### 4xx：客户端错误，请求包含语法错误或无法完成请求;

- #### 5xx：服务器错误，服务器在处理请求的过程中发生了错误;

#### 常见的状态码及含义如下所示：
- #### 200 OK：表示客户端请求成功;

- #### 304 Not Modified：表示服务器告诉客户端，原来缓存的的资源没有过期，还可以继续使用;

- #### 400 Bad Request：表示客户端请求有语法错误，不能被服务器所理解;
- #### 401 Unauthonzed：表示请求未经授权，该状态代码必须与 WWW-Authenticate 报头域一起使用;
- #### 403 Forbidden：表示服务器收到请求，但是拒绝提供服务，通常会在响应正文中给出不提供服务的原因;
- #### 404 Not Found：请求的资源不存在，例如，输入了错误的URL;

- #### 500 Internal Server Error：表示服务器发生不可预期的错误，导致无法完成客户端的请求;
- #### 501 Not Implemented： 表示服务器无法识别或不支持当前请求所需要的资源;
- #### 503 Service Unavailable：表示服务器当前不能够处理客户端的请求，在一段时间之后，服务器可能会恢复正常;



---
### 参考
http://tools.jb51.net/table/http_request_method
