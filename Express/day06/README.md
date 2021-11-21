### Express实战项目

#### 初始化项目

* 创建文件夹

  ```
  mkdir 文件名
  ```

* 进入文件夹

  ```
  cd 文件名
  ```

* 初始化`package.json`文件

  ```
  npm i -y
  ```

* 安装Express

  ```
  npm i express
  ```

* 编写`app.js`代码

  ```js
  // 引入Express 
  const express = require('express');
  
  // 创建express实例
  const app = express();
  
  // 端口号,优先从环境变量中选择, 如果环境变量中没有,就设置为3000
  const PORT = process.env.PORT || 3000;
  
  app.get("/",(req,res) => {
      res.send("GET /");
  })
  
  app.listen(PORT,(req,res) => {
      console.log(`Server is running at http://localhost:${PORT}`);
  })
  ```

#### 创建目录结构

```
.
|-- app.js
|-- config				   # 配置文件
|   |-- config.default.js
|-- controller  		   # 解析用户的输入,处理后返回相应的结果
|-- middleware			   # 用于编写中间件函数
|-- model				   # 数据持久层
|-- router				   # 用于配置URL路由
|-- util 				   # 工具模块
```

#### 配置常用中间件

* 解析请求体
  *  <font color='cornflowerblue'>express.json()</font>
  * <font color='cornflowerblue'>express.urlencoded()</font>
* 日志输出
  * <font color='cornflowerblue'>morgan()</font>
* 为客户端提供跨域资源请求
  * <font color='cornflowerblue'>cors()</font>

#### 路由设计

https://github.com/gothinkster/realworld/tree/main/api

