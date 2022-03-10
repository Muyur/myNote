# 为3个按钮依次绑定函数

## 方法一:匿名函数自调

* 把 i 的作用域限定在匿名函数内，也就是变成局部变量，局部变量在执行完毕后，会自动释放
````js
for(var i=0;i<button.length;i++){
    (function (i) {
            button[i].onclick = function(){
            alert(i+1);
        }
})(i);
````
## 方法二:使用let
* let会把变量的作用域限定在当前代码块内
````js
for(let i = 0;i < button.length;i++){
    button[i].onclick = function(){
        alert(i+1);
    };
}
````
## 方法三:定义对象的属性
````js
for(var i = 0;i < button.length;i++){
    // 为每个对象绑定num属性
    button[i].num = i;
    button[i].onclick = function(){
        alert(this.num+1);
        // 绝了,但是记得用this调用
    };
}
````