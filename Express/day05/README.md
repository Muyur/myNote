### RESTful接口设计规范

#### 协议

API与用户的通信协议,尽量使用https协议(更加安全)

#### 域名

应该尽量将API部署在专用域名下面

```http
https://api.example.com
```

如果确定API很简单,不会有进一步扩展,可以考虑放在主域名下面

```http
https://example.org/api/
```

#### 版本

应该将API的版本号放在URL中

```http
https://api.example.com/v1/
```

另一种做法是,将版本号放在http头信息中,但是不如放在URL中直观方便

(Github采用的便是此方法)

#### 请求路径

路径又称为"终点"(endpoint),表示API的具体网址

在`RESTful`架构中,每个网址代表一种资源(resource),所以<font color='cornflowerblue'>网址中不能有动词,只能有名词</font>,而且所用的名词往往与数据库的表格对应。一般来说,数据库中的表都是同种记录的"集合"(collection),所以API中的名词应该也使用复数。

举例 : 

> 有一个API提供动物园(zoo)的信息,还包括各种动物和雇员的信息,则它的路径一般设计成下边这样

```
https://api.example.com/v1/zoos
https://api.example.com/v1/animals
https://api.example.com/v1/employees
```

#### HTTP动词

对于资源的具体操作类型,由HTTP动词表示

**常用的HTTP动词**有下面五个(括号里是对应的SQL命令)

* GET (读取) : 从服务器取出资源(一项或者多项)
* POST (创建) : 在服务器中新建一个资源
* PUT (完整更新) : 在服务器中更新资源 (客户端提供改变后的完整属性)
* PATCH (部分更新) : 在服务器更新资源(客户端提供改变的属性)
* DELETE (删除) : 从服务器中删除资源

不常用的HTTP动词

* HEAD : 获取资源的元数据
* OPTIONS : 获取信息,关于资源的哪些属性是客户端可以改变的

举例 :

* GET /zoos : 列出所有的动物园
* POST /zoos : 新建一个动物园
* GET /zoos.ID : 获取某个指定动物园的信息
* PUT /zoos/ID : 更新某个指定动物园的信息(提供该动物园的全部信息)
* PATCH /zoos/ID : 更新某个指定动物园的信息(提供该动物园的部分信息)
* DELETE /zoos/ID : 删除某个动物园
* GET /zoos/ID/animals : 列出某个指定动物园的所有动物
* DELETE /zoos/ID/animals/ID : 删除某个指定动物园的指定动物

#### 过滤信息

如果记录数量很多,服务器不可能将它们都返回给用户,API应该提供参数,过滤返回结果

下列是常用参数(都是通过查询字符串的方式来提供的)

* `?limit=10` : 指定返回记录的数量
* `?offset=10` : 指定返回记录的开始位置
* `?page=2&per_page=100` : 指定第几页,以及每页的记录数
* `?sortby=name&order=asc` : 指定返回结果按照哪个属性排序,以及排序顺序
* `?animal_type_id=1` : 指定筛选条件

参数的设计允许存在冗余,即允许API路径和URL参数偶尔有重复,比如,`GET /zoo/ID/animals` 与 `GET /animals?zoo_id=ID` 

#### 状态码

客户端每一次请求,服务器都必须给出回应,回应包括HTTP状态码和数据两部分

HTTP状态码就是一个三位数,分为五个类别

* `1xx` : 相关信息
* `2xx` : 操作成功
* `3xx` : 重定向
* `4xx` : 客户端错误
* `5xx` : 服务器错误

这五大类总共包括100多种状态码,覆盖了绝大部分可能用到的情况,每一种状态码都是有标准的(或者有约定的)解释,客户端只需要查看状态码,就可以判断发生了什么情况,所以客户端应该返回尽可能精确的状态码

常见的状态码

> 幂等性 : 对同一个系统，使用同样的条件，一次请求和重复的多次请求对系统资源的影响是一致的

* `200 OK -[GET]` : 服务器成功返回用户请求的数据,该操作是幂等的(Idempotent)
* `201 CREATED - [POST/PUT/PATCH]` : 用户新建或者修改数据成功
* `202 Accepted - [*]` : 表示一个请求已经进入后台排队(异步任务)
* `204 NO CONTENT - [DELETE]` : 用户删除数据成功
* `400 INVALID REQUEST - [POST/PUT/PATCH]` : 用户发出的请求有错误,服务器没有进行新建或者修改数据的操作,该操作是幂等的
* `401 Unauthorized - [*]` : 表示用户没有权限(令牌,用户名,密码错误)
* `403 Forbidden - [*]` : 表示用的得到授权(与401错误相对),但是访问被禁止了
* `404 NOT FOUND - [*]` : 用户发出的请求针对的是不存在的记录,服务器没有进行操作,该操作是幂等的
* `406 Not Acceptable - [GET]` : 用户请求的格式不可得到 (比如用户请求JSON格式,但是只有XML格式)
* `410 Gone - [GET]` : 用户请求的资源被永久删除,且不会再得到

* `500 INTERNAL SERVER ERROR - [*]` : 服务器发生错误,用户无法判断发送的请求是否成功

#### 返回结果

API返回的数据格式,不应该是纯文本,而应该是一个JSON对象,因为这样才能返回标准的结构化数据,所以,服务器回应的HTTP头的`Content-Type`属性要设置为`application/json`

针对不同的操作,服务器向用户返回的结果应该符合以下**规范**

![image-20211119224400054](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211119224400054.png)

#### 错误处理

有一种错误处理,即使发生错误,也返回200状态码,但是把错误信息放在数据体里面,如下 :

```json
HTTP/1.1 200 OK
Content-Type: application/json

{
    "status":"failure",
    "data": {
        "error": "Expected at least two items in list."
    }
}
```

在上述代码中,解析数据体以后,才能得知操作失败

这种方法实际上取消了状态码,这是完全不可取的,正确的做法是,状态码反应发生的错误,具体的错误信息放在数据体里面返回, 如下

```json
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
    "error": "Invalid payoad",
    "detail": {
        "surname": "This field is required."
    } 
}
```

#### 身份认证

基于 [JWT](https://jwt.io/) 的接口权限认证

> JSON Web Token（缩写 JWT）是目前最流行的跨域认证解决方案
>
> [JSON Web Token 入门教程](http://www.ruanyifeng.com/blog/2018/07/json_web_token-tutorial.html)

* 字段名: `Authorzation`
* 字段值: `Bearer token数据`

#### 跨域处理

可以在服务端设置 [CORS](http://www.ruanyifeng.com/blog/2016/04/cors.html) 允许客户端跨域资源请求















