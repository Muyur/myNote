### 路由路径

#### 基于字符串匹配路径

* 匹配根路径

```js
app.get("/",(req,res) => {
    res.send("GET /")
})
```

* 匹配`/about`路径

```js
app.get("/about",(req,res) => {
    res.send("GET /about")
})
```

* 匹配`index.text`路径

```js
app.get("/index.text",(req,res) => {
    res.send("GET /about")
})
```

#### 基于字符串模式匹配路由路径

* 该路径会匹配`/acb`和`/abcd`

```js
app.get("/ab?cd",(req,res) => {
    res.send("GET /ab?cd");
})
```

* 该路径会匹配`/abc`,`/abbc`,`abbbc` ...

```js
app.get("/ab+c",(req,res) => {
    // + 路径中需要有一个及以上的b
    res.send("/GET /ab+c");
})
```

* 此条路径将会匹配`/abc`,`ab___c`...

```js
app.get("/ab*c",(req,res) => {
    // * 表示任意的
    res.send("GET /ab*c");
})
```

* 该路径匹配`/abcd`或者`/ad`

```js
app.get("/a(bc)?d",(req,res) => {
    res.send("GET /a(bc)?d");
})
```

#### 基于正则表达式匹配路由路径

* 此路由路径将匹配名称中具有“a”的所有路由

```js
app.get(/a/,(req, res) => {
  res.send('/a/');
})
```

* 该路由路径将匹配以`end`结尾的路由

```js
app.get(/.*end$/, function(req, res) {
  res.send('GET /.*end$/');
});
```

