### 路由中的应对方法

* `res.download()`  提示要下载的文件
* `res.end()` 结束响应过程
* `res.json()` 发送`JSON`响应
* `res.jsonp()` 发送带有`JSONP`支持的响应
* `res.redirect()` 重定向请求
* `res.render()` 渲染视图模板
* `res.send()` 发送各种类型的响应
* `res.sendFile()` 将文件作为八位字节流发送
* `res.sendStatus()` 设置响应状态码,并将响应状态码以字符串形式发送为响应正文

### app.route()

> 可以为路由路径创建可链接的路由处理程序`app.route()`,由于路径是在单个位置指定的,因此创建模块化路由是非常有帮助的,对减少冗余和错别字有帮助

使用定义的链式路由处理程序

```js
app.route('/user').get((req,res) => {
    res.send("GET /user");
}).post((req,res) => {
    res.send("POST /user");
}).put((req,res) => {
    res.send("PUT /user");
})
```

### 快速路由器

> 使用`express.Router`,该类创建模块化的,可安装的路由处理程序,一个`Router`实例是一个完整的中间件和路由系统,因此,它通常被称为"迷你应用程序"

示例 : 创建一个名为`router.js` 的文件,文件内容如下

```js
const express = require('express');
const router = express.Router();

router.use((req,res,next) => {
    console.log("now Time: ",Date.now());
    next();
})

router.get("/",() => {
    res.send("GET /");
})

router.post("/about",(req,res) => {
    res.send("POST /about");
})

module.exports = router;
```

在`app.js`文件中引用

```js
const router = require("./router");
// ...
app.use("/router",router);
```

上面代码可以处理`/router`和`/router/about`的请求,以及调用`router.js`的中间件