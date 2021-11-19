### 中间件函数

中间件可以在不修改源代码的情况下修改功能

在中间件中可以执行以下代码

1. 执行任何代码
2. 修改`request`或`response`响应对象
3. 结束相应周期
4. 调用下一个中间件

示例

```js
app.use((req,res,next) => {
    // req.method 请求方法
    // req.url 请求路径
    console.log(req.method,req.url);
    // 可以在中间件中定义函数或者参数等,在请求中调用
    res.print = () => {
        console.log("路由中间件");
    }
    // 如果当前的中间件功能没有请求结束(res.end()),则必须调用next()将控制权传给下一个中间件,否则该请求将会被挂起
    next();
})
```

在`GET`请求中调用`res.print()`

```js
app.get("/",(req,res) => {
    res.print();
    res.send("GET /");
})
```

### 路由中间件分类

> 如果要从路由组件中间件堆栈中跳过其余中间件功能,可以调用`next("route")`跳过当前路由剩余的所有中间件
>
> PS : `next("route")`仅在使用`app.METHOD()`或者`router.METHOD()`函数加载的中间件中有效

* 应用程序级别中间件

  * 不关心请求路径,不做任何限定的中间件

    ```js
    app.use((req,res,next) => {
        console.log("不关心请求路径,不做任何限定的中间件");
        next();
    })
    ```

  * 限定请求路径的中间件

    ```js
    app.use("/about",(req,res,next) => {
        console.log("限定请求路径为/about");
        next();
    })
    ```

  * 限定请求方法和请求路径

    请求路径有 : `GET` , `POST` , `PUT `, `PATCH` , `DELETE` 等

    ```js
    app.get("/about",(req,res,next) => {
        console.log("限定请求路径为/about,请求方法为GET");
        next();
    })
    
    app.post("/home",(req,res,next) => {
        console.log("限定请求路径为/home,请求方法为POST");
        next();
    })
    ```

    

* 路由级别中间件

* 错误处理中间件

* 内置中间件

* 第三方中间件



















