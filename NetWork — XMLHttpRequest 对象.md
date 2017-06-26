# XMLHttpRequest 对象
#### XMLHttpRequest 对象的属性和方法
> JavaScript 就是通过对 XMLHttpRequest 对象的各个属性进行设置来实现 Ajax 的。 




#### XMLHttpRequest Level
##### XMLHttpRequest Level 1主要存在以下缺点：
###### 1. 受同源策略的限制，不能发送跨域请求；
###### 2. ==不能发送二进制文件（如图片、视频、音频等），只能发送纯文本数据；==
###### 3. 在发送和获取数据的过程中，无法实时获取进度信息，只能判断是否完成；

##### 那么Level 2对Level 1 进行了改进，XMLHttpRequest Level 2中新增了以下功能：

###### 1. 可以发送==跨域请求==，在服务端允许的情况下；
###### 2. 支持发送和接收二进制数据；
###### 3. 新增formData对象，支持发送表单数据；
###### 4. 发送和获取数据时，可以==获取进度信息；==
###### 5. 可以设置请求的==超时时间；==


```
/* 通过XMLHttpRequest 构造一个 Ajax 请求 */
function sendAjax() {
  //构造表单数据
  var formData = new FormData();
  formData.append('username', 'johndoe');
  formData.append('id', 123456);
  //创建xhr对象 
  var xhr = new XMLHttpRequest();
  // 添加请求头X-Requested-With，表明是 Ajax 请求
  xhr.setRequestHeader('X-Requested-With', 'XMLHttpRequest');
  /* 如果后面追加 xhr.setRequestHeader('X-Requested-With', 'test');
  最终request header中"X-Requested-With"为:XMLHttpRequest, test */
  
  //设置xhr请求的超时时间
  xhr.timeout = 3000;
  //设置响应返回的数据格式
  xhr.responseType = "text";
  //创建一个 post 请求，采用异步
  xhr.open('POST', '/server', true);
  //注册相关事件回调处理函数
  xhr.onload = function(e) { 
    if(this.status == 200||this.status == 304){
        console.log(this.response); // 获取响应的内容
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
      // e.total是需要传输的总字节，event.loaded是已经传输的字节。
      // 如果 event.lengthComputable 不为真，则 event.total 等于0
  };
  // 断网时，send方法会报错
  try {
      //发送数据，如果是 GET 请求数据放在url里，这里为null
      xhr.send(formData);
      // 另外，这里使用formData 类型的数据后会自动设置 xhr 的 content-type 为 "multipart/form-data"
  } catch(e) {
      
  }
  
  // 取消请求连接
  xhr.abort();
}
```

#### 跨域 Ajax 请求 
##### XDR (IE 8-9 Only)


#### 参考
##### https://segmentfault.com/a/1190000004322487
##### http://www.cnblogs.com/tianyuchen/p/5594641.html