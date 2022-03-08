## Ajax

### 原生Ajax

#### Ajax 简介

* Ajax 全称为 AsynchronousJavaScript+XML , 就是异步的 JS 和 XML
* 通过 Ajax 可以在浏览器中向服务器发送异步请求 , 最大的优势 : **无刷新获取数据**

* Ajax 不是新的编程语言 , 而是一种将现有的标准组合在一起使用的新方式
* 懒加载(按需加载)

#### XML 简介

- XML 可拓展标记语言
- XML 被设计用来传输和存储数据 , HTML 用来呈现数据
- XML 和 HTML 类似 , 不同的是 HTML 中都是预定义标签 , 而 XML 中没有预定义标签

全是自定义标签 , 用来表示一些数据

比如说我有一个学生数据 :

````js
name = "孙悟空";
age = 18;
gender = "男";
````

用 XML 表示 :

````xml
<student>
    <name>孙悟空</name>
    <age>18</age>
    <gender>男</gender>
</student>
````

现在已经被 JSON 取代了

````json
{"name":"孙悟空","age":18,"gender":"男"}
````

#### Ajax 的特点

##### Ajax 的优点

1. 可以无需刷新页面而与服务器端进行通信
2. 允许根据用户事件来更新部分页面内容

##### Ajax 的缺点

1. 没有浏览历史 , 不能回退
2. 存在跨域问题 (同源)
3. SEO 不友好

#### HTTP 协议

HTTP (HyperText Transfer Protocol) 协议 [超文本传输协议] , 协议详细的规定了浏览器和万维网服务器之间相互通信的规则

##### 请求报文

重点是格式与参数

````
行	POST  /s?ie=utf-8  HTTP/1.1
头	Host: baidu.com.com
     Cookie: name=baidu
     Content-type: application/x-www-form-urlencoded
     User-Agent: chrome 83
空行
体	username=admin&password=admin
(如果是GET请求,请求体是空的,如果是POST请求,请求体可以不为空)
````

##### 响应报文

````
行	HTTP/1.1  200 OK
头	Content-Type: text/html;charset=utf-8
	 Content-length: 2048
	 Content-Type: 2048
	 Content-encoding: gzip
空行
体	<html>
		<head>
		</head>
		<body>
			<h1>AJAX</h1>
		</body>
	 </html>
````

#### nodemon

* 网站 [nodemon](https://www.npmjs.com/package/nodemon)

> nodemon is a tool that helps develop node.js based applications by automatically restarting the node application when file changes in the directory are detected.
>
> nodemon does **not** require *any* additional changes to your code or method of development. nodemon is a replacement wrapper for `node`. To use `nodemon`, replace the word `node` on the command line when executing your script.

安装指令

> ```
> npm install -g node
> ```

#### 解决 IE 缓存问题

````js
// 获取当前的时间戳
xhr.open("GET",'http://127.0.0.1:8000/ie?t='+Date.now());
````















 