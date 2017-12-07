### 源
- #### URL
  ##### URL 由协议、域名、端口和路径组成。（protocal + hostName + port + path）
![url结构](https://github.com/StRothschild/NetWork/blob/master/resource/NetWork%20%E2%80%94%20URL.JPG?raw=true)

---
- #### 源
  ##### 如果两个 URL 的协议、域名和端口相同，则表示他们是同源资源。（protocal + hostName + port）


---
- #### 同源策略（same-origin policy）
  > 关键：脚本本身的来源和同源策略并不相关，真正相关的是脚本所嵌入的文档的来源。比如，A 源的脚本在通过 script 标签嵌入 B 源的页面后，则认为脚本是 B 源的，可以读取 B 源的其他文档和内容，而不能读取 A 源的文档和内容。

  ##### 1. 脚本不能读取与操作从不同源载入的文档和内容
  ##### 2. 脚本不能在非同源的文档之间传递信息。
  ##### 2. 脚本不能与不同源的服务器通信（Ajax）。



---
- #### 不受同源策略限制的情况
  ##### html 中的可以获取静态资源的标签，比如 \<script> 中的 src (获取JavaScript脚本) 、\<link> 中的 href (获取CSS) 和 \<img> 中的 src (获取图片)，还有 \<iframe> 中的 src。


---
- #### 不严格的同源策略（非同源的操作即是跨域操作）
  ##### 1. 通过设置文档的 document.domain 属性来避免同源策略（1）的限制
  ###### 在默认情况下 document.domain 的值是当前文档的来源主机名（hostName）。如果把两个不同源的文档设置成相同的 document.domain，则可以认为这两个文档是同源文档，而不受同源策略（1）的限制。

  ##### 2. 通过跨文档消息（cross-document messaging）来避免同源策略（2）的限制
  ###### 通过 window 对象的 postMessage(data, origin) 方法和 onmessage 事件监听可以用异步的方式实现在不同源文档间的文本信息传递。

  ##### 3. 通过跨域资源共享（Cross-Origin Resource Sharing）来避免同源策略（3）的限制
  ###### 跨域资源共享是通过请求头 origin，和返回头 Access-Control-Allow-Origin / Access-Control-Allow-Methods / Access-Control-Allow-Headers 等来实现的。简单的说，就是在跨域请求中添加一个 origin 的字段，来表明跨域请求的来源。然后浏览器通过返回结果的一些控制字段来决定是将结果返回给客户端脚本读取。如果在服务器中没有配置 cors，则返回结果就没有控制字段，浏览器会自动屏蔽脚本对返回信息的读取。
  
  
  
  
---
- #### JSONP（JSON with Padding）
  ##### 为了避免同源策略，可以使用JSONP的方式来获得非同源的JSON数据。其本质是利用了同源策略的例外情况（利用script标签）。
  ```html
  // 由于 JSONP 接口返回的是一个函数调用，并且这个调用会立即执行，所以在此处先行定义函数
  <script>
      function callbackFunctionName(data) {
           // do somthing about data
      }
  </script>
  // 通过 script 标签发送请求，jsoncallback 参数用于指定请求成功后返回的函数的名称，此名称需要与之前定义的函数名相同
  <script src="http://foo.com/jsonpData?jsoncallback=callbackFunctionName"></script>


  // 后端针对上例中 jsonpData 接口实现返回内容如下：
  callbackFunctionName(jsonData);
  ```
