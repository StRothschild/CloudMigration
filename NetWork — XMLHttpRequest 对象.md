# XMLHttpRequest 对象
#### XMLHttpRequest 对象的属性和方法
> JavaScript 就是通过对 XMLHttpRequest 对象的各个属性进行设置来实现 Ajax 的。


- #### XMLHttpRequest Level
  ##### XMLHttpRequest Level 1主要存在以下缺点：
  ###### 1. 受同源策略的限制，不能发送跨域请求；
  ###### 2. ==不能发送二进制文件（如图片、视频、音频等），只能发送纯文本数据；==
  ###### 3. 在发送和获取数据的过程中，无法实时获取进度信息，只能判断是否完成；



- #### 那么Level 2对Level 1 进行了改进，XMLHttpRequest Level 2中新增了以下功能：
  ###### 1. 可以发送==跨域请求==，在服务端允许的情况下；
  ###### 2. 支持发送和接收二进制数据；
  ###### 3. 新增formData对象，支持发送表单数据；
  ###### 4. 发送和获取数据时，可以==获取进度信息；==
  ###### 5. 可以设置请求的==超时时间；==


```javascript
/* 通过XMLHttpRequest 构造一个 Ajax 请求 */
function sendAjax() {
  //构造表单
  var formData = new FormData();
  //如果 form 是页面 DOM 中的表单元素，也可直接作为 formData 的构造参数
  var formData = new FormData(form);
  // 往 formData 中手动添加数据
  formData.append('username', 'johndoe');
  formData.append('id', 123456);

  //创建xhr对象
  var xhr = new XMLHttpRequest();
  //设置xhr请求的超时时间
  xhr.timeout = 3000;
  //设置响应返回的数据格式
  xhr.responseType = "text";

  /* 注册完成事件回调处理函数，相当于 readystate == 4 时触发 */
  xhr.onload = function(e) {
    if(this.status == 200 || this.status == 304) {
        // 当 responseType 为"text" 或 ""时，用此属性获取返回值
        console.log(this.responseText);
        // 返回值要 JSON 对象时，可以调用
        JSON.parse(this.responseText);
        // 当 responseType 为"text"、"" 或 "document"时，才用此属性获取返回值
        console.log(this.responseXML);
    }
  };
  /* 用于请求超时的回调事件 */
  xhr.ontimeout = function(e) {console.log(e);};
  /* 用于请求报错的回调事件 */
  xhr.onerror = function(e) {console.log(e);};
  /* 用于上传的回调事件 */
  xhr.upload.onprogress = function(e) {console.log(e);};
  /* 用于下载的回调事件 */
  xhr.onprogress = function(e) {
      // event.lengthComputable 属性表示进度数据是否可计算
      if(e.lengthComputable) {
        console.log(e.totalSize / e.total); // totalSize / total 表示根据响应头部属性 Content-Length 确定的预期字节数
        console.log(e.position / e.loaded);  // position / loaded 表示已经接收的字节数
      }
  };


  /* 创建一个 post 请求，采用异步 */
  xhr.open('POST', '/server', true);

  // 在设置请求头（requestHeader）时，必须是在 xhr 对象的 opent 方法和 send 方法之间
  /* 添加请求头X-Requested-With，表明是 Ajax 请求 */
  xhr.setRequestHeader('X-Requested-With', 'XMLHttpRequest');
  /* 如果后面追加 xhr.setRequestHeader('X-Requested-With', 'test');
  最终request header中"X-Requested-With"为:XMLHttpRequest, test */


  // 断网时，send方法会报错，可以放在 try-catch 结构中
  try {
      //发送数据，如果是 GET ，请求数据放在 url 里，send 方法里不要参数
      var url = "?" + encodeURIComponent(name) + "=" + encodeURIComponent(value)
      xhr.send();
      //发送数据，如果是 POST，需要在 send 的时候添加数据
      xhr.send(formData);
      // 另外，如果这里使用 formData 类型的数据作为参数有一个好处，就是 xhr 对象会自动识别 fromData 数据类型并且设置 content-type 为 "multipart/form-data"
  } catch(e) {

  }

  // 取消请求连接
  xhr.abort();
}
```



---
- #### readystate
  ##### 0 : 默认值，未初始化。
  ##### 1 : 启动，调用 open 方法。
  ##### 2 : 发送，调用 send 方法。
  ##### 3 : 接收，已接收到部分响应数据。
  ##### 4 : 完成，已接收到所有响应数据。




  ---
- #### XMLHttpRequest 对象会被自动填充的属性
  ##### responseText : 作为响应主体返回的文本。
  ##### responseXML : 如果响应的内容类型是 "tet/xml" 或 "application/xml" 时，这个属性将保存返回的 XML 文档。
  ##### status : 响应的 HTTP 状态。
  ##### statusText :  响应的 HTTP 状态说明。




---
- #### 跨域 Ajax 请求
  ##### XDR (IE 8-9 Only)




---
### 参考
##### https://segmentfault.com/a/1190000004322487
##### http://www.cnblogs.com/tianyuchen/p/5594641.html
