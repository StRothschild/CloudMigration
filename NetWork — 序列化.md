# 网络传输的序列化

### 为什么要将数据序列化？
##### 程序中的==对象状态（简单理解就是数据）往往是有跨平台和跨环境传递的需求的==，比如说 Web 的前后端通信，对象状态的持久化等等。为了兼容不同的平台和环境，数据往往要被转化为两个通信平台都可以理解的数据类型。==将对象状态从内存中读取并转化为通用数据类型（字节流、JSON、XML）的过程，就叫序列化。==
>注意：序列化针对的是对象（引用类型），而不是基本类型。

```
/* 例一：环境中的对象如果直接返回，其实只是内存地址，所以必须先序列化 */
// 在返回对象的 model 中塞入一个没有序列化的对象
model.addAttribute("testProperty", testObject);
// 尝试打印这个对象，发现它只是一个 JVM 虚拟的内存地址
System.out.println(testObject);
// 输出结果：com.netease.haitao.testObject@388671ce
```



---
### 序列化的类型有哪几种？
##### 在 Java 环境中，有多种序列化类型。比较常见的有：Java 原生的 Object Serialize，JSON，XML 等等。如果要在 Java 中实现 JSON 或 XML 序列化，是有许多第三方工具可以使用的，比如 fastjson，jackson 和 dom4j 等等。以下是常见的序列化方式对比图：
![序列化方式对比图](https://github.com/StRothschild/NetWork/blob/master/resource/NetWork%20%E2%80%94%20%E5%BA%8F%E5%88%97%E5%8C%96%E6%96%B9%E5%BC%8F%E5%AF%B9%E6%AF%94.png?raw=true)



---
### Web 前后端的序列化
##### ==在 Web 中通常使用 JSON 来序列化对象，实现前后端的数据交互==。因为 JSON 格式在 JavaScript 中是原生的对象表示法，可以直接调用 JSON.stringify 和 JSON.parse() 两个接口在前端实现对象的序列化和反序列化。另外，在后端的 Java 等环境中，也有很好的第三方支持。



---
### JSON 的序列化
##### 为了避免上文例一中返回一个对象地址的情况出现，需要在返回对象前，给对象进行 JSON 序列化操作。==所谓的 JSON 序列化，就是把 JavaScript 对象变成 JSON 字符串的一个过程。所谓的反序列化，则是把 JSON 字符串还原成 JavaScript 对象。==
```
/* 在 Java 中, JsonUtil 包里封装了一些 JSON 操作方法。比如 toJson 就是把对象序列化成 JSON 字符串 */
model.addAttribute("testProperty", JsonUtils.toJson(testObject));


/* 前端的 JSON 序列化操作 */
JSON.stringify(object)  // 将 JavaScript 中的 object 对象序列化成 JSON 字符串
JSON.parse(string)      // 将 JSON 字符串反序列化成 JavaScript 的对象
```


---
### JSON
##### JSON 值只有 6 种：
- ###### 对象（在花括号中）
- ###### 数组（在方括号中）
- ###### 数字（整数或浮点数）
- ###### ==字符串（在双引号中）==
- ###### 逻辑值（true 或 false）
- ###### null

##### 注意：JSON 字符串和 JSON 对象是不同的概念。==JSON 字符串就是普通字符串，但是符合 JSON 的规范==。而 JSON 对象是 JavaScript 的原生对象，包含用于序列化和反序列化 JSON 的方法。这个对象本身不能被调用或者作为构造函数，除了它的两个方法属性，它没有本身没有什么有用的功能。
```
/* 将 JavaScript 的值序列化为 JSON 字符串 */
JSON.stringify({t:"1", 0:5, a:["d",8]})  // "{"0":5,"t":"1","a":["d",8]}"
JSON.stringify({a:{b:{c:[1, 2, 3]}}})    // "{"a":{"b":{"c":[1,2,3]}}}"
// 注意 JSON 字符串中的 key 必须是字符串（而且必须用双引号），而 value 只要符合上述6种类型即可

/* 从 JSON 字符串中反序列化出 JavaScript 的值 */
JSON.parse("{"0":5}");  // 报错，字符串中不能嵌套两对双引号，会有歧义
JSON.parse('{"0":5}');  // 解析正确，因为 JSON 字符串的 key 必须在双引号中，所以外面的只能包单引号
```


##### 由于 JavaScript 与 JSON 还是存在一定差异的，所以同一个 JavaScript 值在经过 JSON.stringify() 和 JSON.parse() 两个方法后，部分属性可能发生变化。相当于是做了一次深拷贝（deep copy），下图是 JavaScript 与 JSON 的差异表：
![JavaScript 与 JSON 的差异表](https://github.com/StRothschild/NetWork/blob/master/resource/NetWork%20%E2%80%94%20JavaScript%20%E4%B8%8E%20JSON%20%E7%9A%84%E5%8C%BA%E5%88%AB.png?raw=true)
