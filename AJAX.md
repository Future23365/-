# AJAX

### XMLHttpRequest对象的方法

| 方法                                                         | 描述                                      |
| ------------------------------------------------------------ | ----------------------------------------- |
| abort()                                                      | 停止当前请求                              |
| getAllResponseHeaders()                                      | 作为字符串返回完整的headers               |
| getResponseHeader("headerLabel")                             | 作为字符串返回单个header标签              |
| open("method", "URL"[,anysncFlah[,"userName"[,"password"]]]) | 设置未决的请求的目标url，方法，和其他参数 |
| send(content)                                                | 发送请求                                  |
| setRequestHeader("label", "value")                           | 设置header并和请求一起发送                |

### XMLHttpRequest对象的属性

| 属性            | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| onreadystatecha | 状态改变的事件触发器                                         |
| readyState      | 对象状态：0=请求未初始化；1=服务器连接已经建立；2=请求依已接收；3=请求处理中；4=请求已完成，且响应已就绪 |
| responseText    | 服务器进程返回的文本版本                                     |
| responseXML     | 服务器进程返回数据的兼容DOM和XML文档对象                     |
| atatus          | 服务器返回的状态码，如：404=“文件未找到”、200=“成功          |
| statusText      | 服务器返回的状态的文本信息                                   |

**使用AJAX步骤：**

1. 创建一个异步对象
2. 设置请求方式和请求地址
3. 发送请求
4. 监听状态的变化
5. 处理返回的结果

~~~ javascript
encodeURLComponent(字符串);		//这个方法把中文转换为字符型，因为URL不可以传中文
~~~

**两种数据传输用的语言**

1. XML
2. JSON

如果php后端传递XML时有中文需要加下列代码：

~~~ php
header("content-type:text/xml; charset=utf-8");
~~~

**cookie**

| cookie作用: |                                                              |
| ----------- | ------------------------------------------------------------ |
|             | 将网页中的数据保存到浏览器中                                 |
|             |                                                              |
|             | cookie生命周期:                                              |
|             | 默认情况下生命周期是一次会话(浏览器被关闭)                   |
|             | 如果通过expires=设置了过期时间, 并且过期时间没有过期, 那么下次打开浏览器还是存在 |
|             | 如果通过expires=设置了过期时间, 并且过期时间已经过期了,那么会立即删除保存的数据 |
|             |                                                              |
|             | cookie注意点:                                                |
|             | cookie默认不会保存任何的数据                                 |
|             | cookie不能一次性保存多条数据, 要想保存多条数据,只能一条一条的设置 |
|             | cookie有大小和个数的限制                                     |
|             | 个数限制: 20~50                                              |
|             | 大小限制: 4KB左右                                            |
|             |                                                              |
|             | cookie作用范围:                                              |
|             | 同一个浏览器的同一个路径下访问                               |
|             | 如果在同一个浏览器中, 默认情况下下一级路径就可以访问         |
|             | 如果在同一个浏览器中, 想让上一级目录也能访问保存的cookie, 那么需要添加一个path属性才可以; |
|             | document.cookie = "name=zs;path=/;";                         |
|             |                                                              |
|             | 例如:                                                        |
|             | 保存到了www.it666.com/jQuery/Ajax/路径下,                    |
|             | 我们想在 www.it666.com/jQuery/Ajax/13-weibo/,                |
|             | 和 www.it666.com/jQuery/ 路径下也能访问                      |
|             |                                                              |
|             | 例如:                                                        |
|             | 我们在www.it666.com下面保存了一个cookie,                     |
|             | 那么我们在edu.it666.com中是无法访问的                        |
|             | 如果想在edu.it666.com中也能访问, 那么我们需要再添加一个domain属性才可以; |
|             | document.cookie = "name=zs;path=/;domain=it666.com;";        |

### 模板引擎

地址：https://aui.github.io/art-template/zh-cn/docs/

### 同源跨域

**同源：**协议一样，地址一样，端口号一样

**跨域:**不同源的网站之间互相发送请求

浏览器默认限制跨域访问

解决方法： 

1 cors 		HTML5才支持

​	在后端头部设置

~~~ php
herder("Access-Control-Allow-Orign:*")
~~~

2 JSONP

原理：利用的是script标签的src属性 支持跨域访问

用法：script标签后面写上需要请求的页面，发送了一个方法的名字到服务器，服务器接收到方法的名字之后拼接一个方法的调用，在参数中传入需要给浏览器的数据，返回给浏览器，浏览器当做js解析

**知识点**

Jquery中的JSONP原理：动态创建一个SCRIPT标签，利用src发送请求，获取数据

JSONP不能发送post请求

jsonp和ajax没有关系