# Express

> 基于Node的web开发框架

Express网站 :

* [Express官网](http://expressjs.com/)
* [Express中文文档](https://www.expressjs.com.cn/)
* [Github仓库](https://github.com/expressjs/express)

安装Express :

1. 初始化`package.json`文件

   ```
   npm init -y
   ```

2. 安装Express到项目

   ```
   npm i express
   ```

## 基本路由

路由结构的定义 :

```js
app.METHOD(PATH, HANDLER);
```

* app : express实例
* METHOD : HTTP请求方法
* PATH : 服务端路径
* HANDLER : 当路由匹配到时需要执行的处理函数

### 基本的路由请求方法

* GET
* POST
* PUT 
* DELETE
* PATCH

Express基本代码示例 :

```js
const express = require('erpress');
// 获取一个express实例
const app = express();
// GET方法请求
app.get('/get',(req,res) => {
    res.send("GET /get");
})
// POST请求
app.get('/post',(req,res) => {
    res.send("POST /post");
})
// PUT请求
app.get('/put',(req,res) => {
    res.send("PUT /put");
})
// DELETE请求
app.get('/delete',(req,res) => {
    res.send("DELETE /delete");
})
// 监听端口号,启动服务
app.listen(3000,() => {
    console.log("3000端口已启动");
})
```

