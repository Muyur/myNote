# 1. 字面量和变量
* 字面量,不可改变的量
* 变量可以用来改变自变量,可以任意改变,方便使用
* 开发中一般使用变量来保存一个自变量
* var 声明变量
* 可以通过变量对自变量进行描述

# 2. 标识符
在JS中所有的可以由我们自主命名的都可以成为标识符
1. 标识符中可以含有字母,数字,_,$
2. 标识符不能以数字开头
3. 标识符不能是ES中的关键字或保留字,如var,if
4. 标识符一般都采用驼峰命名法
- 首字母小写,每个单词的开头字母大写,其余字母小写

![](2021-03-11-21-10-55.png)

# 3. 字符串
* 字符类型:字面量的类型
1. String 字符串
2. Number 数值
3. Boolean 布尔型
4. Null 空值
5. Undefined 未定义
6. Object 对象
* 其中String,Number,Boolean,NUll,Undefined属于基本数据类型
* Object属于引用数据类型
## 3.1. String 字符串
* 需要使用时用引号引起来,但是不能混着用
* 引号不能嵌套,双引号里面不能放双引号,单引号里面不能用单引号
* 或者用符号表示,转义字符,如:   \"   \'   \n   \\

````html
var str1 = "I say\"Who are you?\""
var str2 = "Hello"
<!-- 输出字面量str2 -->
console.log("str2");
<!-- 输出变量str2 -->
console.log(str2);
````
## 3.2. Number 数值
typeof操作符返回变量,对象,函数,表达式的类型
在 JS 中所有的数据都是Number类型
## 3.3. 强制类型转换
![](2021-03-12-10-05-26.png)
强制一个数据类型转换为其他数据类型
### 3.3.1. 将其他数据类型转换为String
* 方式一:
调用被转换数据类型的toString()方法
该方法不会影响原变量,它会将转换的结果返回
但是注意:null和undefined这两个值没有toString()方法,如果调用他们,会报错
````js
var a = 123;
a = a.toString();
document.write(typeof a + "<br>" + a);
````
* 方式二:
调用String()函数,并将被转换的数据作为参数传递给函数
使用String()函数做强制类型转换时,对于Number和Boolean实际上就是调用toString()方法
但是对于null和undefined,就不会调用toString()方法
它会将null直接转换为"null",将undefined直接转换为"undefined"
````js
var x = 123;
x = String(x);
document.write(typeof x + "<br>" + x);
````
### 3.3.2. 调用Number()函数来将a转换为Number类型
1. 转换方式一:
* 如果是纯数字的字符串,则直接将其转换为数字
* 如果字符串中有非数字的内容,则转换为NaN
* 如果字符串是一个空串或者是一个全是空格的字符串,则转换为0
* 如果是布尔类型,true转成1,false转成0
* Null转换成0
* undefined转换成0
````js
var a = "123";
a = Number(a); 
console.log(typedef a); //number
console.log(a);  //123
````
2. 转换方式二(专门对付字符串)
* parseInt 将字符串转换成整数
读到非数字立即停止
````js
var a = "123b456c";
// 但是第一个字符不是数字的话就会转换成NaN
a = parseInt(a);
document.write(typeof a + "<br>" + a);
// 结果为 a = 123
````
可以将一个字符串中的有效的整数取出来,然后转换成Number
* parseFloat 可以获得字符串中有效的小数
````js
// 但是第一个字符不是数字的话就会转换成NaN
var b = "123.456.789ab7";
b = parseFloat(b);
document.write(typeof b + "<br>" + b);
// 结果 b = 123.456
````

对非String使用parseInt()或parseFloat(),它会先将其转换成String再进行操作

## 3.4. 转换成布尔类型
将其他的数据类型转换成Boolean
- 使用Boolean()函数
````js
a = 123;
a = Boolean(a);
document.write(typeof a + "<br>" + a);
````
* 对于Number,除了0和NaN,其他的都是true
* 对于String,除了空串,其余都是true
* null 和 undefined 转换成 Boolean 型都是 false
* 对象 Object 也会转换成 true
# 4. 其他进制的数字
* 如果需要表示十六进制的数字,则需要以0x开头
````js
var a = 0x10;
var b = 0xff;
var c = 0xCafe;
document.write(a + "<br>" + b + "<br>" + c);
````
* 如果需要表达八进制的数字,则需要以0开头
````js
var x = 012;
var y = 0556;
var z = 070;
document.write(x + "<br>" + y + "<br>" + z);
````
* 如果需要表达二进制的数字,则需要以0b开头,但并不是所有浏览器都支持
````js
var p = 0b10;
var q = 0b11;
var r = 0b00101;
document.write(p + "<br>" + q + "<br>" + r);
````
* 转换成字符串时
````js
var a = "080";
a = parseInt(a);
document.write(typeof a + "<br>" + a);
// 部分浏览器当作八进制转换,为56,部分浏览器当作十进制转换,为70
````
解决方法如下:在parseInt()传递第二个参数,来指定数字的进制
````js
var a = "080";
a = parseInt(a,10);
document.write(typeof a + "<br>" + a);
````
![](2021-03-12-19-53-48.png)

# 5. 运算符/操作符
可以通过运算符对一个值或多个值进行运算并获得运算结果
* typeof 运算符
可以获得一个值的类型,将该值的类型以字符串的类型返回

* 加法(+)
当对非Number类型的值进行运算时,会将这些值转换为Number然后再运算
1. true = 1;
2. false = 0;
3. null = 0;
4. 任何值和NaN进行运算,结果都是NaN
5. 如果对字符串进行运算,会进行拼串.
````js
var a = "123";
var b = "456";
c = a + b;
document.write(c);
// c = 123456
````
6. 任何值和字符串进行加法运算,都会先转换为字符串,然后进行拼串
(利用这一特点,来将一个任意的数据类型转换为String)
(只需要在任意数据类型加上一个""即可将其转换为String)
(隐式类型转换)
按照顺序进行运算,顺序很重要
````js
result = 1 + 2 + "3";
// result = 33;
````

````js
result = "1" + 2 + 3;
// result = 123;
````

````js
result = 1 + "2" + 3;
// result = 123;
````
* 减法(-)
都是先转换成Number型再进行运算
(利用这一特点,来将一个任意的数据类型转换为Number)
(只需要在任意数据类型减去一个0即可将其转换为Number)
(隐式类型转换)
````js
result = 100 - "1";
// 得出 result = 99;
````
* 取模运算 *(取余数)

# 6. 一元运算符
(只需要一个操作数)
* 正号 +(不会对数字产生任何影响)
可以对一个其它的数据类型使用+使其转换为Number型
原理和Number函数一样
````js 
var x = "18";
x = +x;
// x = 18
// typeof x = number
````

````js
result = 1 + +"2" + 3;
// result = 6;
````
* 负号 -(可以对数字进行符号的取反)
* 对于非Number类型的值,它会将其转换为Number类型后再运算
````js 
var x = "18";
x = -x;
// x = -18
// typeof x = number
````

# 7. 自增和自减
* 自增 ++
通过自增可以使变量在原来的基础上+1
````js
++i;
i++;
````
不论是++i还是i++都会使原变量立即自增1
i++ 的值等于原变量的值(自增前的值)
````js
var x =  10;
document.write(x++);
// x = 10
````
++i 的值等于原变量的值+1(自增后的值)
````js
var x =  10;
document.write(++x);
// x = 11
````
一个变量自增后,原变量会立即自增1
* 自减 --
通过自增可以使变量在原来的基础上-1
````js
i--;
--i;
````
i-- 的值等于原变量的值(自减前的值)
````js
var y =  10;
document.write(y--);
// y = 10
````
--i 的值等于原变量的值-1(自减后的值)
````js
var y =  10;
document.write(--y);
// y = 9
````

# 8. 逻辑运算符
* !     非(对一个布尔值进行取反操作)
如果对一个值进行两次取反(!!a)它不会变化
如果对一个非布尔型进行此操作,会先将其转换成布尔型,然后再取反
所以我们可以利用该特点,来将一个其他的数据类型转换成布尔型
![](2021-03-12-19-54-42.png)
````js
var b = 10;
b = !!b;
document.write(b);
````
* &&    与
可以对符号两侧的值进行与运算并返回结果
如果两端都是true,则返回true
只要有一个false,就返回false
````js
var result = true && true;
document.write(result);
````
* ||    或
只要有一个true,就返回true
如果两个都是都是false,则返回false
````js
var result = true || false;
document.write(result);
````
1. 如果第一个是false,则会检查第二个
````js
false || alert("123");
````
2. 如果第一个是true,则不再检查第二个
````js
true || alert("123");
````

# 9. 非布尔值的与或运算
### 9.0.1. && 与运算
对于非布尔值进行与或运算,会先将其转换成布尔型,然后再运算,但是返回原值.
1. 与运算如果两个值都为true,则返回后者
````js
var result = 1 && 2;
document.write(result);
// result = 2
````

2. 如果两个值一个是true,一个是false,则返回false
````js
var result = 0 && 2;
document.write(result);
// result = 0
````

3. 如果两个值都是false,则返回前者
````js
var result = 0 && NaN;
document.write(result);
// result = 0
````

4. 总结
只要第一个值为true,就返回第二个值

### 9.0.2. || 或运算
1. 如果两个值都是true,则返回第一个
````js
var result = 3 || 2;
document.write(result);
// result = 3
````
2. 如果有一个值为false,另一个值为true,则返回true
````js
var result = 0 || 7;
document.write(result);
// result = 7
````
3. 如果两个值都为false,则返回第二个
````js
var result = 0 || NaN;
document.write(result);
// result = NaN
````
4. 总结:只要第一个为false,一定返回第二个

# 10. = 赋值运算符
可以将符号右侧的值赋值给符号左侧

# 11. 关系运算符
通过关系运算符可以比较两个值之间的大学
如果关系成立则返回true,如果关系不成立则返回false
* / > 大于
````js
result = 5 > 10;
document.write(result);
// result = false
````
* / >= 大于等于
````js
result = 10 >= 10;
document.write(result);
// result = true
````
* / < 小于
````js
result = 10 < 10;
document.write(result);
// result = false
````
* / <= 小于等于
````js
result = 7 <= 7;
document.write(result);
// result = true
````
* == 等于
````js
result = 10 = 10;
document.write(result);
// result = true
````
## 11.1. 非数值的情况
* 对于非数值的比较,会先将其转换成数值然后再进行比较
````js
result = 1 >= true;
document.write(result);
// result = true
````
````js
result = 5 > "10";
document.write(result);
// result = false
````
````js
result = 10 > null;//0
document.write(result);
// result = true;
````
* 任何值和NaN做任何比较都是false
````js
// 如果字符串中有非数字的内容,则转换为NaN
result = 10 > "hello";//NaN
document.write(result);
// result = false;
````
````js
result = true > false;
document.write(result);
// result = true
// true -- 1
// false -- 0
````
* 如果符号两边都是字符串时,不会将其转换为数字进行比较,而是分别比较字符串中字符的Unicode编码(ASCII)
````js
result = "abc" > "b";
document.write(result);
// result = false
````
* 比较字符编码时,是一位一位进行比较,如果两位一样,则比较下一位
````js
result = "bbc" > "b";
document.write(result);
// result = true
````
* 如果比较的两个字符串型的数字,可能会得到不可预期的结果
````js
result = "11" > "5";
document.write(result);
// result = flase
````
* 比较中文没有意义hehe

# 12. Unicode编码表
````js
var result = "\u1c00"
document.write(result);
````
* 在网页中使用&#编码
这里的编码需要的是十进制
````html
<h1>&#9777;</h1>
````
# 13. 相等运算符
## 13.1. == 相等
当使用==来进行比较时,如果值的类型不同,会自动进行类型转换,将其转换成相同的类型
````js
var result = 1 == "1";
document.write(result);
// result = true
````

````js
var result = null == 0;
document.write(result);
// result = false
````
* undefined 衍生自 null ,二者做==判断时会返回true
````js
var result = null == undefined;
document.write(result);
// result = true
````
* NaN不和任何值相等,包括它本身
````js
var result = NaN == NaN;
document.write(result);
// result = false
````
#### 13.1.0.1. 判断一个值是否等于NaN
通过isNaN()函数比较
````js
var a = NaN;
document.write(isNaN(a));
// result = true
````
## 13.2. != 不相等
如果不相等返回true,否则返回false
当使用!=来进行比较时,如果值的类型不同,也会自动进行类型转换,将其转换成相同的类型
## 13.3. === 全等
用来判断两个值是否全等,他和相等类似,不同的是不会自动进行类型的转换.
如果两个值的类型不同,直接返回false
````js
result = 5 === "5";
document.write(result);
// result = false
````
# 14. 条件运算符(三元运算符)
#### 14.0.0.2. 语法: 条件表达式?语句1:语句2;
执行流程:
1. 对条件表达式进行求值
2. 若该值为true,则返回语句1
3. 若该值为false,则返回语句2
````js
1>2?alert("true"):alert("false");
````
````js
var a = 567;
var b = 79;
var max = a>b?a:b;
document.write(max);
````
* 进行两次判断
这种写法不推荐使用,不方便阅读
````js
var a = 567;
var b = 799;
var c = 13;
var max = a>b?(a>c?a:c):(b>c?b:c);
document.write(max);
````
* 如果条件表达式的结果是一个非布尔型,会将其转换成布尔型,然后再运算
````js
"hello"?alert("true"):alert("false");
// true
````
````js
""?alert("true"):alert("false");
// false
````
# 15. 运算符的优先级
![](2021-03-13-13-32-32.png)
![](2021-03-13-13-33-27.png)
* 如果优先级不清楚,可以使用括号来改变优先级
在js中可以使用{}为语句分组,同一个{}中的语句,要么都执行,要么都不执行
一个{}中的语句也成为代码块,代码块后面不用编写;
JS中的代码块只具有分组作用

# 16. 流程控制语句
js中的程序是从上往下一行一行执行的
* 语句的分类
    1. 条件判断语句
    2. 条件分支语句
    3. 循环语句
## 16.1. 条件判断语句 if
在执行某个语句之前进行判断,如果成立则执行,否则不执行
#### 16.1.0.3. 语法:
    if(条件表达式){
        代码块
    }
    else if(条件表达式){
        代码块
    }
    .
    .
    .
    else{
        代码块
    }
依次向下执行,如果为true则停止,否则继续执行.
该语句中,只有一个代码块会被执行,一旦代码块被执行,则结束该语句
````js
if(7 > 9){
    alert("true");
}
else{
    alert("false");
}
````
````js
var age = 67;
if(age < 18){
    alert("你还未成年!");
}
else if(age<60){
    alert("你还在中年!!");
}
else{
    alert("你该退休了!!!");
}
````
## 16.2. var score = prompt("请输入小明的成绩:"); 可以用来输入
````js
var score = prompt("请输入小明的成绩:");
// 先判断成绩是否超出范围,是否为函数
if(score > 100 || score < 0 || isNaN(score)){
    alert("出错了!!!");
}
else{
    if(score == 100){
        alert("奖励你一辆BWM");
    }
    else if(score > 90){
        alert("奖励你一台 iphone 15s");
    }
    else if(score >80){
        alert("奖励你一本参考书");
    }
    else{
        alert("你真么也没有");
    }    
}
````
# 17. switch 语句
1. 
````js
var score = prompt("请输入成绩:");
// 取整数
switch(parseInt(score/60)){
    case 1:{
        alert("及格");
        break;
    }
    case 0:{
        alert("不及格");
        break;
    }
}
````
2. 
````js
var score = prompt("请输入成绩:");
// 成立则执行代码块
switch(true){
    case score >= 60:
        alert("及格");
        break;
    default:
        alert("不及格");
        break;
}
````
# 18. 循环语句
1. for
````js
var n = 7;
for(var i = 1;i <= n;i++)
{
    document.write(i + "<br>");
}
````
````js
var sum = 0;
for(var i = 1;i <= 100;i++)
{
    sum += i;
}
document.write(sum);
````
2. while
    * 先判断后执行
````js
var n = 7,i = 1;
while(i <= n)
{
    document.write(i + "<br>");
    i++;
}
````

````js
var money = 1000,n = 0;
// 定义一个计数器
while(money < 5000){
    money *= 1.05;
    n++;
}
document.write(n + "<br>" + money);
````
*将条件表达式写死为true的循环,称为死循环
这种循环不会停止,除非浏览器关闭
如果手贱写了死循环,解决方案:
在敲回车键的同时按下浏览器的关闭键❌
多来几次
3. do...while
    * 可以保证循环体至少执行一次,先执行后判断
````js
var n = 7,i = 1;
do
{
    document.write(i + "<br>");
    i++;
}
while(i <= n)
````

# 19. 水仙花数
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        var i;
        for(i = 100;i < 1000;i++){
            var a = parseInt(i/100);
            var b = parseInt((i-a*100)/10);
            var c = i%10;
            if(a*a*a+b*b*b+c*c*c == i){
                document.write(i + "<br>");
            }
        }
    </script>
</body>
</html>
````
# 20. 判断是否为质数
1. 
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        var num = prompt("请输入一个大于1的整数:");
        var flag = 0;
        if(num <= 1){
            alert("数字不合法");
        }
        else{
            for(var i = 2;i < num;i++){
                if(num % i == 0){
                    flag = 1;
                    break;
                }
            }
            if(flag == 1){
                alert("该值不是质数");
            }
            else{
                alert("该值是质数")
            }
        }
    </script>
</body>
</html>
````
2. 布尔型
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        var num = prompt("请输入一个大于1的整数:");
        var flag = true;
        if(num <= 1){
            alert("数字不合法");
        }
        else{
            for(var i = 2;i < num;i++){
                if(num % i == 0){
                    flag = false;
                    break;
                }
            }
            if(flag){
                alert(num + "该值是质数");
            }
            else{
                alert(num + "该值不是质数")
            }
        }
    </script>
</body>
</html>
````
# 21. 打印***

````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        var n = prompt("请输入一个数字:");
        for(var i = 1;i <= n;i++){
            for(var j = 1;j <= i;j++){
                document.write("*");
            }
            document.write("<br>");
        }
        for(var i = n-1;i > 0;i--){
            for(var j = 1;j <= i;j++){
                document.write("*");
            }
            document.write("<br>");
        }
    </script>
</body>
</html>
````
## 21.1. break
可以用来退出switch或者循环语句
会立即终止离它最近的那个循环
````js
for(var i = 0;i < 5;i++){
    document.write(i + "<br>");
    if(i == 2){
        break;
    }
}
````
## 21.2. continue
````js
for(var i = 0;i < 5;i++){
    if(i == 2){
        continue;
    }
    document.write(i + "<br>");
}
````
# 22. 对象的简介
1. JS中的数据类型
    * String 字符串
    * Number 数值
    * Boolean 布尔型
    * Null 空值
    * Undefined 未定义
-- 以上五种类型属于基本数据类型
-- 只要不是以上五种,都是对象
-- 基本数据类型都是单一的值,值和值之间没有任何联系
-- 如果使用基本数据类型的数据,我们所创建的变量都是独立的,不能成为一个整体
2. Object 对象
* 对象属于一种复合的数据类型
* 在对象中可以保存多个不同数据类型的属性
* 对象的分类
    1. 内建对象
    - 由ES标准中定义的对象,在任何的ES的实现中都可以使用
    - 比如:Math String Number Boolean Function Object...
    2. 宿主对象
    - 由JS的运行环境提供的对象,目前来讲主要指由浏览器提供的对象
    - 比如 BOM,DOM
    3. 自定义对象
    - 由开发人员自己创建的对象
### 22.0.1. 自定义对象
1. 创建对象
* 使用new关键字调用的函数,是构建函数constructor
* 构造函数是专门用来创建对象的函数
* 在对象中保存的值称为属性
* 读取对象中的属性
    - 语法: 对象.属性名
    - 如果读取对象中没有的属性,不会报错而会返回undefined
    - 修改对象属性值: 对象.属性名=新值
    - 删除对象属性值: delete 对象.属性值
    ````js
    var obj = new Object();
    obj.name = "Han dog";
    obj.gender = "female";
    obj.age = 80;
    obj.name = "Han shouo"
    delete obj.name;
    document.write(obj.name);
    // cao想起了链表的增删查改
    ````
    - 不强制要求遵守标识符的规范
    - 如果要使用特殊的属性名,不能采用.的方式来操作
    - 需要使用另一种形式:
        - 语法: 对象["属性名"] = 属性值

        ````js
        obj["123"] = 567
        document.write(obj["123"]);
        ````
#### 22.0.1.1. 使用[]这种形式去操作属性,更加灵活
在[]中可以直接传递一个变量,这样变量值是多少就会去读那个属性
````js
obj["123"] = 567
var n = "123";
document.write(obj[n]);
````
##### 22.0.1.1.1. in 运算符
通过该运算符,可以检查一个对象中是否含有指定属性
如果有则返回true,否则返回false
* 语法:
    "属性名: in 对象
````js
obj.name = "Han dog";
document.write("name" in obj);
````
# 23. 基本数据类型和引用数据类型
* 基本数据类型:
    String Number Boolean Null Undefined
* 引用数据类型:
    Object
````js
var obj = new Object;
obj.name = "13";
obj2 = obj;
obj.name = "567";
document.write(obj.name + "<br>");
document.write(obj2.name);
// 二者指向同一个对象
// obj.name变化,obj2.name也会随之变化
````
js中的基本数据类型变量都是保存到栈内存中的,修改一个变量不会影响其他的变量.
引用数据类型(对象)保存在堆内存中,没创建出一个新的对象,都会在堆内存中开辟一块新的空间.
如果两个变量保存的是同一个对象，当一个通过变量修改属性时，另一个也会受到影响
如果修改的是第二个变量，则第一个变量的属性不会改变，即切断了第二个变量与对象之间的联系
![](2021-03-14-13-43-54.png)
定义的两个变量对象也不同，故二者不相等
当比较两个基本数据类型是，就是比较二者的值，而比较两个引用数据类型时，就是比较的对象的内存地址，如果两个对象一模一样，但是内存地址不同，也会返回false
````js
var obj = new Object;
obj.name = "13";
var obj2 = new Object;
obj2.name = "13";
document.write(obj == obj2);
// 返回false
````
# 24. 对象字面量
````js
var obj = new Object();
var obj = {};
// 其本质是一样的
````
* 使用对象字面量时，可以在创建对象时，直接指定对象中的属性
    语法：{属性名：属性值，属性名：属性值...};
````js
var obj = {name:"Han",age:80,color:yellow};
````
对象字面量的属性名可以加引号也可以不加，建议不加
如果要使用一些特殊的名字，则必须加引号
名和值只见使用：链接，多个名值对之间使用，隔开
如果一个属性之后没有其他的属性，就不要写，
````js
var obj = {
    name:"FuShu",
    age:18,
    gender:"Male",
    test:{fname:"SY"}
    // 此处不能使用等于号=
}
````

# 25. 函数Function
* 函数也是一个对象
* 函数中可以封装一些功能（代码），在需要的时候执行这些功能（代码）
* 函数中可以保存一些代码，在需要时进行调用
    - 创建一个函数对象
    - 可以将要封装的代码以字符串的形式传递给构造函数
    - 封装到函数中的代码不会立即执行
    - 函数中的代码会在函数调用的时候执行
    - 调用函数语法，函数对象（）
    - 当调用函数时，函数中的代码会按照顺序执行
````js
var fun = new Function("alert('Hello World!');"); 
// 双引号里面不能再添加双引号
//可以将要封装的代码以字符串的形式传递给构造函数
fun();
````
#### 25.0.1.2. 函数对象具有所有普通法对象所具有的功能
````js
var fun = new Function(); 
fun.name = "FuShu";
alert("fun.name");
````
在开发中很少使用构造函数来创建一个函数对象
### 25.0.2. 使用函数声明来创建一个函数
    语法： function 函数名（参数1，参数2...）{}
````js
function fun2{
    alert("Hello World!");
}
fun2();
````
### 25.0.3. 使用函数表达式来创建一个函数
语法: var 函数名 = function(形参1，形参2...){}
````js
var fun3 = function(){
    alert("Hello World!");
}
fun3();
````
````js
function sum(x,y){
    z = x + y;
    alert(z);
}
sum(1,2);
````
* 注意是否会接收到非法的实参,如果有可能,则需要对参数进行类型的检查
* 调用函数时，解析器也不会检查实参的数量
* 多余实参不会被赋值
* 如果传入的实参的数量少于形参的数量，则没有对应实参的形参将是undefined
# 26. 返回值
* 可以使用return来获得返回值
return可以作为函数的执行结果返回
````js
function sum(a,b,c){
    return (a+b+c);
}
document.write(sum(5,6,7));
````
在函数中,return后面的语句都不会执行
````js
var r = prompt("请输入r的值");
function S(r){
    s = 3.14 * r * r;
    return s;
}
alert(S(r));
````

````js
var x = prompt("请输入x的值:");
function isOu(num){
    if(num % 2 == 0){
        return true;
    }
    else{
        return false;
    }
}
alert(isOu(x));
````
### 26.0.4. 调用函数 函数()|function()
- 相当于使用函数的返回值
### 26.0.5. 函数对象 函数|function
- 相当于直接使用函数对象

#### 26.0.5.1. 返回值可以是任意的数据类型,也可以是一个对象,还可以是一个函数
````js
function fun1(){
    // 在函数内部再声明一个函数
    function fun2(){
        alert("Hello World!");
    }
    return fun2();
}
var a = fun1();
// 以下两种表述都相当于调用了fun2
fun1()();
a();
````
# 27. 立即执行函数
#### 27.0.5.2. 语法:(函数(){})();
````js
// 函数对象()
// 立即执行函数往往只会执行一次,没有变量去保存它
// 可以调用匿名函数
(function(){
    alert("Hello World");
})();
(function(a,b){
    document.write("a = " + a + "<br>");
    document.write("b = " + b);
})(1,2);
````
#### 27.0.5.3. 对象的属性值可以是任何的数据类型,也可以是个函数
- 函数也可以称为对象的属性,如果一个函数作为一个对象的属性保存,那么我们成这个函数为这个对象的方法,调用函数即调用对象的方法,但是它只是名称上的区别,没有其他区别
1. 
````js
var obj = new Object;
obj.name = "Fu Shu";
obj.age = 18;

obj.sayName = function(){
    alert(obj.name);
};
obj.sayName();
````
2. 
````js
var obj = {
    name:"Fu Shu",
    age:18,
    sayName:function(){
        alert(obj.name);
    }
}
obj.sayName();
````
# 28. 枚举对象中的属性
使用 for ... in 属性
* 语法:
    for(var 变量 in 对象)
对象中有几个属性,循环体就会执行几次
每次执行时,会将对象中的一个属性赋值给变量
````js
var obj = {
    name:"Fu Shu",
    age:19,
    address:"Xuanwu Conutry",
}
for(var n in obj){
    alert(n);
    // 有点数组的味儿了
    alert(obj[n]);
}
````
# 29. debug
````js
alert("Hello World!");
debugger;
alert("I am FuShu");
alert("且将新火试新茶")
````

# 30. this 属性
解析器在调用函数每次都会向函数内部传递进一个隐含的参数
这个隐含的参数就是this,this指向的是一个对象
这个对象称为函数执行的上下文对象
根据函数调用方式的不同,this会指向不同的对象
- 以函数形式调用时,this永远都是window
- 以方法形式调用时,this就是调用方法时的那个对象
````js
function fun(){
    alert(this.name);
}
var obj1 = {
    name:"Fu shu",
    sayname:fun
};
var obj2 = {
    name:"Qi",
    sayname:fun
};
obj1.sayname();
````
# 31. 使用工厂方法创建对象
通过该方法可以大批量创建对象
1. 创建含有需要属性的函数
2. 通过多次调用函数来批量创建对象
````js
function createPerson(name,age,adress){
    var obj = new Object;
    // 向对象中添加属性
    obj.name = name;
    obj.age = age;
    obj.adress = adress;
    return obj;
}
var obj1 = createPerson("Fu shu",19,"XW");
var obj2 = createPerson("Qi",21,"XW");
var obj3 = createPerson("aLu",21,"XW");
var obj4 = createPerson("Qing",17,"XW");
alert(obj1);
````
# 32. 构造函数
* 构造函数就是一个普通的函数,创建方式和普通函数没有区别
* 构造函数习惯上首字母大写
* 普通函数是直接调用,构造函数需要使用new关键字来调用
    1. 立即创建一个新的对象
    2. 将新建的对象设置为函数中this
    3. 逐步执行函数中的代码
    4. 将新建的对象作为返回值返回
* 使用同一个构造函数创建的对象,成为一类对象,也将一个构造函数称为一个类
我们将通过一个构造函数创建的对象,称为该类的实例
#### 32.0.5.4. 使用instanceof 可以检查一个对象是否是一个类的实例
##### 32.0.5.4.1. 语法: 对象 instranceof 类;
* 如果是,则返回true
* 如果不是,则返回false
* 所有的对象都是object的后代,所以任何对象和object做instranceof检查时都会返回true
##### 32.0.5.4.2. this 的情况
1. 当以函数的形式调用时,this就是window
2. 当以方法的形式调用时,谁调用方法this就是谁
3. 当以构造函数的形式调用时,this就是新创建的那个对象
# 33. 原型对象
使用in检查对象中是否含有某个属性时,如果对象中没有但是原型中有,也会返回true
````js
function MyClass(){

}
MyClass.prototype.name = "我是原型中的名字";
var mc = new MyClass();
document.write("name" in mc);
// true
````
可以使用对象的hasOwnProperty()来检查对象自身中是否含有该属性
使用该方法,只有对象本身中含有属性时,才会返回true
````js
function MyClass(){

}
MyClass.prototype.name = "我是原型中的名字";
var mc = new MyClass();
document.write(mc.hasOwnProperty("name"));
// false
````
__proto__指的是对象的原型
原型对象也是原型,所以也有原型
自身中如果有,则直接使用
如果没有,则去原型对象中寻找,如果原型对象中有,则使用
如果没有,则去原型的原型中寻找,直到找到Object对象的原型
Object对象的原型没有原型
如果在Object中依然没有找到,则返回undefined
````js
function MyClass(){

}
MyClass.prototype.name = "我是原型中的名字";
var mc = new MyClass();
document.write(mc.__proto__.hasOwnProperty("hasOwnProperty"));
// false
````
这尼玛谁着的住
````js
function MyClass(){

}
MyClass.prototype.name = "我是原型中的名字";
var mc = new MyClass();
document.write(mc.__proto__.__proto__.hasOwnProperty("hasOwnProperty"));
````
# 34. toString
当我们直接在页面上打印一个对象时.时间上是输出的对象的toSiring()方法的返回值
如果我们希望再输出对象的时候不输出[object Object],可以为对象添加一个toString()方法
````js
function Person(name,age,gender){
    this.name = name;
    this.age = age;
    this.gender = gender;
}
var per = new Person("柒",21,"男");
document.write(per);
````

````js
function Person(name,age,gender){
    this.name = name;
    this.age = age;
    this.gender = gender;
}
var per = new Person("柒",21,"男");
per.toString = function(){
    return "Person[name="+this.name+",age="+this.age+",gender="+this.gender+"]";
};
var result = per.toString();
// document.write(result);
document.write(per);
````
修改Person原型的toString
````js
function Person(name,age,gender){
    this.name = name;
    this.age = age;
    this.gender = gender;
}
Person.prototype.toString = function(){
    return "Person[name="+this.name+",age="+this.age+",gender="+this.gender+"]";
};
var per = new Person("柒",21,"男");
var per2 = new Person("玖",19,"女");
// per.toString = function(){
//     return "Person[name="+this.name+",age="+this.age+",gender="+this.gender+"]";
// };
// var result = per.toString();
// document.write(result);
document.write(per + "<br>");
document.write(per2);
````

# 35. 垃圾回收（GC)
程序运行过程中会产生垃圾
当一个对象没有任何的变量或属性对他进行引用时，此时我们将永远无法操作该对象
此时这种对象就是一个垃圾
JS中有自动的垃圾回收机制，会自动将这种垃圾对象从内存中销毁
我们不需要也不能进行垃圾回收的操作
我们需要做的只是将不再使用的对象设置null即可

# 36. 数组(Array)
和普通的对象功能一致,也是用来存储某些值的
而数组使用元素是使用数字来作为索引操作元素
从0开始的整数就是索引
数组的存储性能比普通对象要好,在开发过程中我们经常使用数组来存储一些数据
* 内建对象
* 数组对象
* 自定义对象
如果读取不存在,不会报错,而是返回undefined
````js
var arr = new Array;
arr[0] = 10;
arr[1] = 5;
arr[2] = 6;
document.write(arr);
````
获取数组的长度(元素的个数)
语法: 数组.length
对于连续的数组,使用length可以获取到数组的长度(元素的个数)
对于不连续的数组,数组长度会获得最大索引+1
尽量不要创建非连续数组
修改length
如果修改的length 大于原数组,则多余的地方会空出来
如果修改的length小于原数组,则多余的元素会被删除
````js
var arr = new Array;
arr[0] = 10;
arr[1] = 5;
arr[2] = 6;
document.write(arr.length);
````
依次递增
````js
var arr = new Array;
arr[0] = 10;
arr[1] = 5;
arr[2] = 6;
arr[3] = 7;
arr[4] = 13;
arr[arr.length] = 20;
arr[arr.length] = 30;
arr[arr.length] = 40;
arr[arr.length] = 50;
document.write(arr
````
使用字面量创建数组时,可以在创建时就指定数组中的元素
````js
var arr = [1,2,3,4,5,6,7]
document.write(arr);
document.write("<br>" + arr.length);
````
使用构造函数创建数组时,也可以同时添加元素,将要添加的元素作为构造函数的参数传递,元素之间使用逗号隔开
````js
var arr = new Array(10,20,30);
document.write(arr);
````

````js
// 创建一个数组元素,数组中只有一个元素10
var arr1 = [10];
// 创建一个长度为10的数组
// JS中的数组长度意义不大
// 数组中的元素可以是任意的数据类型
var arr2 = new Array(10);
document.write(arr1 + "<br>" + arr2);
````
数组中的元素可以是任意的数据类型
````js
var arr1 = ["hello",1,true,null,undefined];
````
````js
// 创建一个数组元素,数组中只有一个元素10
var arr = ["hello",1,true,null,undefined];
document.write(arr);
````
也可以是对象
二维数组:数组里面放的还是数组

### 36.0.6. 数字的四个方法
![](2021-03-16-11-07-49.png)
![](2021-06-16-11-12-33.png)
#### 36.0.6.1. 语法:arrayObject.push(newelement1,ewelement2,ewelement3...)
##### 36.0.6.1.1. push() 该方法可以向数组末尾添加一个或多个元素并返回新的数组长度(想起来进栈出栈)
* 可以要传入的元素作为方法的参数传递,这样这些元素会自动添加到数组的末尾
该方法会将数组新的长度作为返回值返回
````js
var arr = ["Qi","Jiu","Shisan","Lu"];
var result = arr.push("Qing","Yue","An");
document.write(arr + "<br>" + result);
````
##### 36.0.6.1.2. pop() 该方法可以删除数组的最后一个元素,并将其值作为返回值返回
````js
var arr = ["Qi","Jiu","Shisan","Lu"];
arr.pop();
document.write(arr);
````
* 返回其值
````js
var arr = ["Qi","Jiu","Shisan","Lu"];
var result = arr.pop();
document.write(arr + "<br>" + result);
````
##### 36.0.6.1.3. unshift() 向数组的开头添加一个或多个元素,并返回新的数组长度
像前面插入元素后,其他元素的索引会依次调整
````js
var arr = ["不","知","身","是","客"];
var result = arr.unshift("梦","里");
document.write(arr + "<br>" + result);
````

##### 36.0.6.1.4. shift() 删除数组的第一个元素并返回其值
````js
var arr = ["Qi","Yue","Fu","Shu","An"];
var result = arr.shift();
document.write(arr + "<br>" + result);
````

````js
var per1 = {name:"Qi",age:21};
var per2 = {name:"Jiu",age:19};
var per3 = {name:"Lu",age:21};
var per4 = {name:"Ran",age:12};
var per5 = {name:"Qing",age:18};
var per6 = {name:"Xia",age:11};
var arr = [per1,per2,per3,per4,per5,per6];
for(var i = 0;i < arr.length;i++)
{
    if(arr[i].age >= 18){
        document.write(arr[i].name + "<br>");
    }
}
````
#### 36.0.6.2. 遍历数组的方法(2) -- forEach
这个方法支支持IE8以上的浏览器,IE8及以下 的浏览器均不支持该方法,如果需要兼容IE8,则不要使用forEach方法,使用for循环来遍历
像这种函数,由我们创建但是不由我们调用的,我们称为回调函数,每次执行时,浏览器会将遍历的元素以实参的形式传递过来,我们可以定义形参,来读取这些内容
浏览器会在回调函数中传递三个参数
- 第一个参数就是我们当前正在遍历的元素
- 第二个参数是当前正在遍历参数的索引
- 第三个参数就是我们正在遍历的这个数组

````js
var arr = ["Yi","Er","San","Si","Wu","Liu","Qi","Ba","Jiu"];
arr.forEach(function(value,index,obj){
    // 创建一个匿名函数
    document.write(value + "<br>");
})
````
# 37. slice 和 splice
### 37.0.7. slice 从某个已有的数组返回选定的元素
#### 37.0.7.1. 语法: arrayObject.slice(start,end)
该方法不会改变元素数组,而是将截取到的元素封装到一个新数组中返回
* [start,end)
1. start 截取开始的位置的索引
2. end 截取结束的位置的索引,第二个参数可以省略不写,此时会直接截取到最后
3. 索引可以传递一个负值,如果传递一个负值,则从后往前计算
    -1 倒数第一个
    -2 倒数第二个
    ...
![](2021-03-16-12-00-28.png)
````js
var arr = ["Yi","Er","San","Si","Wu","Liu","Qi","Ba","Jiu"];
// 截取位置包含开始,不包含结束
var result = arr.slice(0,2);
document.write(result);
````
### 37.0.8. splice 删除元素,并向数组添加新元素
使用splice()会影响到原数组,会将指定的元素删除并作为返回值返回
1. 第一个参数:表示开始的位置
2. 第二个参数:表示删除的个数
3. 第三个及以后的参数:插入新的元素,插入到开始位置的索引前面
````js
var arr = ["Yi","Er","San","Si","Wu","Liu","Qi","Ba","Jiu"];
// 截取位置包含开始,不包含结束
var result = arr.splice(1,2);
document.write(arr + "<br>" + result);
````
后面添上要插入的新元素
````js
var arr = ["Yi","Er","San","Si","Wu","Liu","Qi","Ba","Jiu"];
// 截取位置包含开始,不包含结束
var result = arr.splice(1,2,"ShiSna");
document.write(arr + "<br>" + result);
````

# 38. 数组的剩余方法
![](2021-03-16-20-46-02.png)
* concat()可连接两个或多个数组,并将新的数组返回
    - 语法: 数组1.concat(数组2,数组3...);
    - 该方法不会对原数组产生影响
    - 不仅可以传数组,还可以传元素
````js
var arr = ["Qi","Bai","Qing","Fu","Yan","Jiu"];
var arr2 = ["Mei","Shian","Chi"];
var arr3 = ["San","Wu","Lu"];
var result = arr.concat(arr2,arr3,"Xia");
document.write(result);
````
* join() 把数组的所有元素放入一个字符串,元素通过指定的分隔符进行分隔
    - 该方法可以将数组转换成字符串
    - 该方法不会对原数组产生影响,而是将转换后的字符串作为结果返回
    - 在join()中可以指定一个字符串作为参数,这个字符串会成为数组中元素的连接符
    - 如果不指定连接符,则默认为,
````js
var arr = ["Qi","Bai","Qing","Fu","Yan","Jiu"];
var result = arr.join("-");
// 连接符放在这里
document.write(typeof result + "<br>");
// 类型为string
document.write(result);
````
* reverse() 该方法用来反转数组
    - 该方法会直接修改原数组
````js
var arr = ["Qi","Bai","Qing","Fu","Yan","Jiu"];
var result = arr.reverse();
document.write(result);
````
* sort() 可以用来对数组进行排序
    - 该方法会影响原数组
    - 即使对于纯数字的排序,也会使用Unicode编码进行排序
    - 我们可以在sort中指定一个回调函数,来指定排序规则
    - 回调函数中需要定义两个形参
    - 浏览器会分别使用数组中的元素作为实参去调用回调函数
    - 使用哪个数组元素不确定,但可以肯定的是a一定在b之前
    - 浏览器会根据回调函数的返回值来确定元素的顺序
    - 如果返回一个大于0的值,则元素会交换位置
    - 如果返回一个小于0的值.则元素的位置不变
    - 如果返回值为0,则认为两个元素的值相等,不交换位置
````js
var arr = [11,5,8,9,4,6,7,1,9,3];
arr.sort(function(a,b){
    // 直接定义一个匿名函数
    // if(a > b){
    //     return 1;
    // }
    // else if(a < b){
    //     return -1;
    // }
    // else{
    //     return 0;
    // }
    return a-b;
    // 升序
    retuen b-a;
    // 降序
});
document.write(arr);
````
# 39. call 和 apply 函数的方法
都是函数对象的方法,都需要通过函数对象来调用
当对函数调用call()和apply()都会调用函数执行
在调用call()和apply()时,可以将一个对象指定为第一个参数,
此时这个对象间会成为函数执行时的this
* call() 可以将实参在对象之前以后一次传递
````js

````
* apply() 需要将实参封存到一个数组中同
![](2021-03-16-21-37-06.png)
1. 以构造函数的形式调用,this是新创建的那个对象
2. 使用call和apply调用时this是指定的那个对象

# 40. agrument
- 在调用函数时,浏览器每次都会传递两个隐含的参数
````js
function fun(a,b){
    document.write(arguments.length);
}
fun("hello",true);
````
    1. 函数的上下文对象this
    2. 封装实参的对象arguments
        - arguments 是一个类数组对象
        - 在调用函数时,我们所传递的实参都会封装到arguments中
        - 我们即使不定义形参,也可以使用arguments来使用实参
        只不过比较麻烦
        - arguments.length表示实参的数量
        - arguments[0] 表示第一个实参
        - 他里面有一个属性叫callee
        - 这个属性对应一个函数对象,就是当前正在指向的函数的对象
````js            
function fun(a,b){
document.write(arguments.callee == fun);
}
fun("hello",true);
````
# 41. Date()
- 在JS中使用Date()对象来表示时间
    * 如果直接使用构造函数创建一个Date()对象,则会封装为当前代码执行的时间
````js
var d = new Date();
document.write(d);
````
- 创建一个指定的时间对象
    * 需要在构造函数中传递一个表示时间的字符串作为参数
    * 日期格式:月份/日/年 时:分:秒
        年份写完整避免歧义
        ![](2021-03-17-16-41-48.png)
````js
var d = new Date("2/26/2021 05:06:07");
document.write(d);
````
* Date() 获取当前日期是几日
````js
var d = new Date("2/26/2021 05:");
document.write(d);
var date = d.getDate();
document.write(date);
````
* Day() 获取当天是周几
    - 会返回一个0-6的值.0表示周日
````js
var d = new Date("2/26/2021 05:06:07");
document.write(d);
var date = d.getDate();
var day = d.getDay();
document.write(date + "<br>" + day);
````
* GetMonth() 会获得当前的月份
    - 会返回一个0-11的数字
    - 0 表示一月,以此类推...11 表示十二月
````js
var d = new Date("3/26/2021 05:06:07");
document.write(d);
var date = d.getDate();
var day = d.getDay();
var month = d.getMonth();
var year = d.getFullYear();
document.write(date + "<br>" + day + "<br>" + month + "<br>" + year);
````
* getFullYear() 获取当前日期的年份
````js
var d = new Date("3/26/2021 05:06:07");
document.write(d);
var date = d.getDate();
var day = d.getDay();
var month = d.getMonth();
var year = d.getFullYear();
document.write(date + "<br>" + day + "<br>" + month + "<br>" + year);
````
* getTime() 获取当前日期的时间戳
    - 时间戳:指的是从1970年1月1日,0时0分0秒到现在所经历的毫秒数
    - 统一单位为毫秒(1秒 = 1000毫秒)
    - 计算机底层在保存时间时使用的都是时间戳
````js
var d = new Date("3/26/2021 05:06:07");
document.write(d);
var date = d.getDate();
var day = d.getDay();
var month = d.getMonth();
var year = d.getFullYear();
var time = d.getTime();
document.write("<br>" + time + "<br>" + date + "<br>" + day + "<br>" + month + "<br>" + year);
````
* 北京时间比格林尼治时间早8h
    中文版本按照中国时间来算
````js
var d1 = new Date("1/1/1970 00:00:00");
var time1 = d1.getTime();
document.write(time1);
-28800000
````
* 获取当前的时间戳
````js
var time2 = Date.now();
document.write(time2);
````
* 可以利用时间戳来测试当前代码的性能

# 42. Math 
    - Math 和其它对象不同,他不是一个构造函数
    - 它属于一个工具类.不用创建对象,它里面封装了数学运算相关的属性和方法
![](2021-03-17-17-22-59.png)
![](2021-03-17-17-23-33.png)
````js
document.write(Math.PI);
````
* abs() 返回数的绝对值
````js
document.write(Math.abs(-567));
````
* Math.ceil() 对数进行上舍入(向上取整,小数位只要有值就自动进1,只对数值有用)
````js
document.write(Math.ceil(5.5));
````
* Math.floor()可以对一个数进行向下取整(小数部分会被舍去,只对数值有用)
````js
document.write(Math.floor(5.67));
````
* Math.round() 对一个小数进行四舍五入(只对数值有用)
````js
document.write(Math.round(5.67));
````
* Math.random() 返回一个0-1之间的随机数
    - 生成一个0-x之间的随机整数
    document.write(Math.round(Math.random()*x));
    - 生成一个x-y之间的随机数
    document.write(Math.round(Math.random()*(y-x)+x));
````js
document.write(Math.random());
// 生成一个0-1的随机数
document.write(Math.random()*10);
// 生成一个0-10的随机整数
document.write(Math.round(Math.random()*10));
````
* max() 可以获取多个数中的最大值
````js
document.write(Math.max(5,8,9,79));
````
* min() 可以获取多个数中的最小值
````js
document.write(Math.min(5,8,9,79));
````
* pow(x,y) 返回x的y次幂
````js
document.write(Math.pow(2,10));
````
* sqrt() 对一个数进行开方
````js
document.write(Math.sqrt(2));
````
# 43. 包装类(是浏览器底层自己用的)
在JS中为我们提供了三个包装类,通过这三个包装类可以将基本数据类型的数据转换成对象
* String()
    - 可以将基本类型字符串转换为String对象
* Number()
    - 可以将基本数据类型的数字转换成Number对象
* Boolean()
    - 可以将基本数据类型的布尔值转换成Boolean对象
* 注意:我们在实际应用中不会使用基本数据类型的对象,
    如果使用基本数据类型的对象,在做一些比较时可能会带来一些不可预料的问题
    对象转为布尔值都是true
    方法和属性只能添加给对象,不能添加给基本数据类型
* 当我们对一些基本数据类型的值去调用属性和方法时,浏览器会来临时使用包装类将其转换为对象,然后再调用对象的属性和方法,调用完之后.再将其转换为基本数据类型
````js
// 创建一个Number类型的对象
var num = new Number(3);
document.write(typeof num);
// 对象中可以添加属性
// 而基本数据类型无法添加属性
num.hello = "abdcid";
document.write(num.hello);
````
````js
var num1 = new Number(3);
var num2 = new Number(3);
document.write(num1 == num2);
// false
// 对象作比较是比较的是对象的地址
document.write("<br>");
document.write(num1 == num3);
// true
// 会自动进行类型转换
````
# 44. 字符串的方法
* 在底层字符串是以字符数组的形式保存的
* length属性
    - 可以用来获得字符串的长度
* charAt()
    - 返回指定位置的字符(不会对原字符串产生影响)
    - 根据索引获得指定的字符
````js
var str = "Hello World!"
document.write(str.length + "<br>");
var result = str.charAt();
document.write(result);
````
* charCodeAt()
    - 返回指定位置的字符的Unicode编码
````js
var str = "Hello World!"
var result = str.charCodeAt();
document.write(result);
````
* fromCharCode()
    - 可以根据字符编码获取字符
````js
var result = String.fromCharCode(72);
document.write(result);
````
* concat() 
    - 可以用来连接两个或多个字符串
````js
var str = "Hello World ! ";
var result = str.concat("I will do it ! ","How are you.");
document.write(result);
````
* indexOf() 
    - 该方法可以检索字符串中是否含有指定内容
    - 如果字符串中含有该内容,会返回该字符第一次出现的索引
    - 若果没有,则返回-1
    - 可以指定第二个参数,用来指定开始查找的位置
````js
var str = "Hello World ! ";
var result = str.indexOf("x",2);
document.write(result);
````
* lastIndexOf()
    - 用法和indexOf()一样,但是不同的是从后往前找
    - 但是返回的还是从前往后找的索引
    - 也可以指定查找位置
````js
var str = "Hello World ! ";
var result = str.lastIndexOf("l",5);
document.write(result);
````
* slice() 
    - 截取字符串
    - 可以从字符串中截取指定内容
    - 不会影响原数组,将截取到的数字返回
    - 参数:
        1. 第一个:开始位置索引(包括开始位置)
        2. 第二个:结束位置索引(不包括结束位置)
        3. 如果不写第二个,则从开始到字符串结束都要,第二个参数可以省略
        4. 也可以传递一个负数作为参数,负数的话会从后面开始
````js
var str = "Hello World ! ";
var result = str.slice(2,5);
document.write(result);
````
* substring
    - 可以用来截取字符串
    - 参数:
        1. 第一个:开始位置索引(包括开始位置)
        2. 第二个:结束位置索引(不包括结束位置)
        3. 不同的是这个方法不能接受负值作为参数,如果传递了一个负值,则默认使用0
        4. 而且它会自动调整参数的位置,如果第二个参数小于第一个参数,则自动交换位置
````js
var str = "Hello World ! ";
var result = str.substring(2,1);
document.write(result);
````
* substr()
    - 用来截取字符串
    - 参数:
        1. 第一个参数:截取开始位置的索引
        2. 第二个参数:截取的长度
        3. 第二个参数忽略时,直接截取到末尾
* split()
    - 可以将一个字符串拆分成数组
    - str.split("") 如果传入一个空串作为参数,则会将整个字符串拆分为一个一个元素,一个字符一个元素
* join("")
    - 可以将一个数组转换成字符串
    - 传入一个空串作为参数
````js
var str = "abc,def,ghi,jil,mno";
var result = str.split(",");
// 根据逗号拆分数组
document.write(result + "<br>" + typeof result + "<br>" + Array.isArray(result) + "<br>" + result[0] + "<br>" + result.length);
````
![](2021-03-18-17-19-58.png)
* toUpperCase()
    - 将字符串转换成大写
    - 不会影响到原字符串
````js
var str = "abcdefghijilmno";
var result = str.toUpperCase();
// 根据逗号拆分数组
document.write(result);
````
* toLowerCase()
    - 将字符串转换成小写
    - 不会影响到原字符串
````js
var str = "ABCDEFGHIJKLMN";
var result = str.toLowerCase();
// 根据逗号拆分数组
document.write(result);
````
# 45. 正则表达式(定义一些字符串规则)
* 计算机可以根据正则表达式来检查一个字符串是否符合规则
* 或者将字符串中符合规则的字符串提取出来
1. 创建正则对象
    - 语法:
    ````js
    var 变量 = new RegExp("正则表达式","匹配模式");
    ````
    - 正则表达式的方法:
        test()
        - 使用这个方法可以用来检查一个字符串是否符合正则表达式的规则
         - 如果符合规则则返回true,否则返回false
````js
var reg = new RegExp("a");
var str = "a";
var result = reg.test(str);
document.write(result);
````

    - 在构造函数中,可以传递一个匹配模式作为第二个参数
    可以是
    1. i 忽略大小写
    2. g 全局匹配模式
````js
var reg = new RegExp("A","i");
var str = "a";
var result = reg.test(str);
document.write(result);
````
* 使用字面量来创建正则表达式
    - 语法: var 变量 = /正则表达式/匹配模式
    - 使用字面量的方式创建更加简单,但是使用构造函数创建更加灵活
````js
var reg = /a/i;
var str = "abd";
var result = reg.test(str);
document.write(result);
````
* 创建一个正则表达式,检查一个字符串中是否含有a或b
    - 使用|表示或者的意思
    - []里面的内容也是或者的意思
        [ab] == a|b
````js
var reg = /a|b/i;
var str = "bcd";
var result = reg.test(str);
document.write(result);
````
* 创建一个正则表达式来检查一个字符串中是否含有字母
    - [a-z] 表示任意小写字母
    - [A-Z] 表示任意的大写字母
    - [A-z] 表示任意字母
````js
var reg = /[a-z]/i;
var str = "123";
var result = reg.test(str);
document.write(result);
````
* 检查一个字符串里是否含有abc或adc或aec
````js
var reg = /a[bde]c/i;
var str = "aec";
var result = reg.test(str);
document.write(result);
````
* [^ ] 表示除了这里面的都行
    - 只要里面有除了ab以外的东西都行
![](2021-03-18-21-23-24.png)
````js
var reg = /[^ab]/i;
var str = "a";
var result = reg.test(str);
document.write(result);
````
# 46. 字符串和正则相关的方法
![](2021-03-18-21-27-13.png)
* split() 可以将字符串拆分成数组
    - 方法中可以传递一个正则表达式作为参数,这样方法会根据正则表达式来拆分字符串
    - 这个方法即使不指定全局匹配,也会全部插分
````js
var str = "1a2b3c4d5e6f7";
var result = str.split(/[A-z]/);
document.write(result);
````
* search()
    - 可以搜索字符串中是否含有指定内容
        - 如果搜索到指定内容,则会返回第一次出现的索引
        - 如果没有搜索到则返回-1
        - 它可以接受一个正则表达式作为参数,然后会根据正则表达式去检索字符串
        - search()只会查找第一个符合要求的内容,即使设置全局匹配也没用
````js
var str = "hello abc hello adc hello aec";
var result = str.search(/a[bde]c/);
document.write(result);
````
* match() 
    - 可以根据正则表达式,从一个字符串中将符合条件的内容提取出来
    - 默认情况下match()只会找到第一个符合要求的内容,找到以后就停止检索
    - 我们可以设置正则表达式为全局匹配模式,这样就会匹配到所有的内容
    - 可以为一个正则表达式设置多个匹配模式,且顺序无所谓
    - match()会将匹配到的内容封装到一个数组中,即使只查询到一个结果
````js
var str = "hello abc hello adc hello aec";
// var result = str.match(/[A-z]/g);
var result = str.match(/[a-z]/ig);
document.write(result);
````
* replace()
    - 可以将字符串中指定的内容替换成新的内容
    - 参数:
        1. 被替换的内容,可以接受一个正则表达式作为参数
        2. 新的内容
    - 默认只会替换第一个087
````js
var str = "hello abc hello adc hello aec";
// var result = str.match(/[A-z]/g);
var result = str.replace(/e/g,"@_@");
document.write(result);
````
# 47. 正则表达式语法
* 量词
    - 通过量词可以设置一个内容出现的次数
    - var reg = /a{3}/; 表示a连续出现3次
    - {n} 正好出现n次
    ````js
    var reg = /a{3}/;
    var str = "aaabbdhcc";
    var result = reg.test(str);
    document.write(result);
    ````
    - 量词只对它前面的一个内容起作用,如/ab{3}/表示abbb
    - /(ab){3}/表示ababab
    ````js
    var reg = /(ab){3}/;
    var str = "abababaabbaba";
    var result = reg.test(str);
    document.write(result);
    ````
    - /ab{1,3}c 表示b出现一次到三次,即abc,abbc或abbbc出现m到n次
    - {m,n} 
    ````js
    var reg = /ab{1,3}c/;
    var str = "abbc";
    var result = reg.test(str);
    document.write(result);
    ````
    - {m,} 表示m次以上
    ````js
    var reg = /ab{3,}c/;
    var str = "abbbbbbbbbbbbbbbbbbbc";
    var result = reg.test(str);
    document.write(result);
    ````
![](2021-03-19-09-56-04.png)
* n+
    - 表示至少一个n,相当于{1,}
    ````js
    var reg = /ab+c/;
    var str = "abbbc";
    var result = reg.test(str);
    document.write(result);
    ````
* n* 
    - 表示0个或多个,相当于{0,}
    ````js
    var reg = /ab*c/;
    var str = "ac";
    var result = reg.test(str);
    document.write(result);
    ````
* n? 
    - 表示0个或1个,相当于{0,1}
    ````js
    var reg = /ab?c/;
    var str = "ac";
    var result = reg.test(str);
    document.write(result);
    ````        
* ^n
    - 检查一个字符串是否以n开头
    ````js
    var reg = /^(abc)/;
    // 这个abc好像不需要括号
    var str = "abcdddddddd";
    var result = reg.test(str);
    document.write(result);
    ````
* n$
    - 检查一个字符串是否以n结尾
    ````js
    var reg = /abc$/;
    // 这个好像也不需要
    var str = "abcddddddddabc";
    var result = reg.test(str);
    document.write(result);
    ````
* 同时使用时
    - 下列方法返回false
    - 该语句表示同一个abc既是开头又是结尾,即语句只能是abc
    - 如果在正则表达式中同时使用^和$,则要求字符串必须完全符合正则表达式
    ````js
    var reg = /^(abc)$/;
    var str = "abcddddddddabc";
    var result = reg.test(str);
    document.write(result);
    // false
    ````
    ````js
    var reg = /^(abc)$/;
    var str = "abc";
    var result = reg.test(str);
    document.write(result);
    // true
    ````
* ^n|$n
    - 以n开头或者以n结尾
    ````js
    var reg = /^abc|abc$/;
    // 以abc开头或者以abc结尾
    var str = "abcaaaababbaabc";
    var result = reg.test(str);
    document.write(result);
    ````
* 检查手机号是否合格
````js
var phoneStr = "15738672079";
var phoneReg = /^1[3-9][0-9]{9}$/
var result = phoneReg.test(phoneStr); 
document.write(result);
````
![](2021-03-19-10-41-24.png)
* . 表示任意字符
   
````js
var phoneStr = "bfvhiygo9";
var phoneReg = /./
var result = phoneReg.test(phoneStr); 
document.write(result);
````
- 在正则表达式中使用\表示转义字符
````js
var phoneStr = "bfv.hiygo9";
var phoneReg = /\./
var result = phoneReg.test(phoneStr); 
document.write(result);
````
````js
var phoneStr = "bfv\\hiygo9";
// 也是转义字符
// 写两个,打印出来是一个
var phoneReg = /\\/
var result = phoneReg.test(phoneStr); 
document.write(result);
````
* 注意:使用构造函数时,由于它的参数是一个字符串,而\是字符串中的转义字符,故如果需要使用\,则用\\来代替
* \w
    - 表示任意字母,数字,_下划线
    - [A-z0-9_]
````js
var str = "abc";
var reg = /\w/;
var result = reg.test(str);
document.write(result);
````
* \W
- 除了数字,字母,_下划线
- [^A-z0-9_]
````js
var str = "*******";
var reg = /\W/;
var result = reg.test(str);
document.write(result);
```` 
* \d
    - 任意的数字[0-9]
    ````js
    var str = "123";
    var reg = /\d/;
    var result = reg.test(str);
    document.write(result);
    ````
* \D
- 除了数字[^0-9]
````js
var str = "abc";
var reg = /\D/;
var result = reg.test(str);
document.write(result);
````
* \s
    - 空格
    ````js
    var str = "Hello 123!";
    var reg = /\s/;
    var result = reg.test(str);
    document.write(result);
    ````
* \S
    - 除了空格
    ````js
    var str = "    ";
    var reg = /\S/;
    var result = reg.test(str);
    document.write(result);
    ````
* \b
    - 单词边界(即单词前后的空格)

    ````js
    var str = "Hello child";
    var reg = /\bchild\b/;
    var result = reg.test(str);
    document.write(result);
    ````
* \B
    - 除了单词边界
* 去除字符串中的前后空格
    - 即使用空串来替换空格
````js
// 这就很神奇???
var str = "              hello child     ";
// 匹配开头和结尾的空格
str = str.replace(/^\s* | \s*$/g,"");
console.log(str);
````
# 电子邮件的正则表达式
* 任意字母数字下划线.任意字母数字下划线@任意字母数字.任意字母.任意字母
* w{3,} (\.\w+)* @ [A-z)-9] + (\.[A-z]{2,5}){1,2}/
# DOM 简介
![](2021-03-19-14-31-52.png)
![](2021-03-19-14-42-10.png)
![](2021-03-19-14-46-41.png)
# 事件的简介
* 在时间对应的属性中设置一些JS代码,这样当事件被触发时,这些代码将会执行
![](2021-03-19-15-08-32.png)
````js
<button onmousemove="alert("别碰老子!");">点我</button>
<p id="demo"></p>
````
* 这种方式称为行为和结构耦合,不方便维护,不推荐使用
* 可以为按钮的对应事件绑定处理函数的形式未响应事件,这样当事件被触发时,其对应的函数将会被调用
* 为单击事件绑定的函数,我们成为单击响应函数
````js
<button ondblclick="myFun()">点我</button>
<p id="demo"></p>
<script>
function myFun(){
    alert("别碰老子!");
    // document.getElementById("demo").innerHTML = "别碰老子!";
}
</script>
````
# 文档的加载
* 浏览器加载页面是按照自上而下的顺序加载的,读取一行就运行一行
# 图片切换
# DOM 查询
![](2021-03-19-19-23-21.png)
* 为id为btn01的按钮绑定一个单机响应函数
* getElementsByTagName()可以根据标签名来获取一组元素节点对象
* innerHTML用于获取标签内部的html代码
* 对于自结束标签,这个属性没有意义
* 如果需要读取元素节点的属性
* 直接使用 元素.属性名
* 但是class属性不能采用这种方式
# 获取元素节点的子节点
![](2021-03-19-21-06-37.png)

![](2021-03-20-10-15-34.png)

![](2021-03-20-11-22-49.png)

# 全选练习

# DOM 查询的其他方法
* 在document中有一个属性叫body,他保存的是body的引用
* document.documentElement保存的是html根标签
* document.all 代表页面中的所有元素
* document.getElementsByTagName("*") 也代表页面中所有元素
### 根据元素的class属性查询一组元素节点对象
### getElementsByClassName("")
* 但是IE9及以上才支持
* document.getElementsByTagName("div") 获取页面中所有的div
* document.querySelector(); 需要一个选择器的字符串作为参数,可以根据一个css选择器来查询一个元素节点对象
* document.querySelectorAll(".box1") 该方法和document.querySelector()用法类似,但是它会将符合要求的结果封装都到数组中返回
    - 即使符合条件的元素只有一个,也会返回数组
![](2021-03-26-14-36-15.png)
### ==**DOM查询**==
PS:重新总结了一下
* **读取元素内的内容**
````js
console.log(idStr.innerHTML);
````
* **读取input内的内容**
````js
console.log(input.value);
````
* **获取某id下的某元素结点,例如:**
````js
var lis = idStr.getElementsByTagName("li");
````
* **获取某id下子结点/子元素**
    - childNodes 获取子结点
        + childNodes属性会获取包括文本节点在内的所有节点
        + 根据DOM标签之间的空白也会当成文本结点
        + 注意:在IE8及以下的浏览器,不会将空白文本当成子文本
        ````js
        var cns = idStr.childNodes;
        // 获取元素子结点
        // 包括DOM标签中的空白结点
        ````
    - children 获取子元素
        + children可以获得当前所有元素的子元素
        ````js
        var cns = idStr.children;
        // 获取子元素
        // 不包括空白结点
        ````
* **获取某元素的兄弟结点/元素**
    - previousSibling 获取前一个兄弟结点
        + 可能是空白结点
        ````js
        var pr = idStr.previousSibling;
        ````
    - previousElementSibling 获取前一个兄弟元素
        + 不会是空白结点
        ````js
        var pr = idStr.previousElementSibling;
        ````
# DOM的增删改
* document.createElement();
    - 可以用于创建一个元素节点对象
    - 他需要一个标签名作为参数,将会根据该标签名创建对象
    - 并将创建好的对象作为返回值返回
* document.createTextNode("");
    - 可以用于创建一个文本节点对象
    - 需要一个文本内容作为参数,将会根据改内容创建文本节点,并将新的节点返回
* appendChild()
    - 向一个父节点中添加一个子节点
    - 语法: 父元素.appendChild(子节点)
* city.insertBefore(li,bj);
    - 可以在指定子节点前插入新节点
    - 语法: 父节点.insertBefore(新结点,旧节点)
* replaceChild
    - 可以使用指定的子节点替换已有的子节点
    - 语法: 父节点.replaceChild(新节点,旧节点)
* removeChild
    - 可以删除一个子节点
    - 语法
        1. 父节点.removeChild(子节点)
        2. 子节点.parentNode.removeChild(子节点);
# a的索引问题

# DOM操作内联样式
* 通过JS修改元素的样式
* 语法：元素.style.样式名 = 样式值
* 如果CSS的元素中含有-，这种名称在JS里是不合法的，比如background-color
* 需要将这种样式名修改为驼峰命名法
* 即去除"-",把后面第一个字母变成大写(backgroundColor)
* 修改的是内联样式(优先级比较高，覆盖了id选择器样式)
* background-color: red !important; !important提高了优先级，不会被内联元素覆盖
* 用了这个之后JS也无法修改此元素
### alert(box1.style.backgroundColor);
* 语法: 元素.style.样式名
* 通过style设置和读取的样式都是内联样式(html文件内样式,不是css中的样式)
* 无法读取样式表中的样式
# 读取元素当前样式
## currentStyle  当前样式?
* 获取元素当前显示的样子 
* 它可以用来读取当前元素正在显示的样式
* 如果当前元素没有设置该样式,则获取该元素的默认样式
* 语法: 
    1. 在IE9及以上(只有IE支持)
        - 元素.currentStyle.样式名
        ````js
        alert(box1.currentStyle.width);
        ````
    2. 在谷歌和火狐及其他浏览器中中
        - getComputedStyle获取当前元素样式
        - 需要额外创建函数
        - 需要两个参数
            1. 第一个元素样式的元素
            2. 第二个元素传递一个伪元素,一般都传null
            3. 不支持IE8及以下
            ````js
            var obj = getComputedStyle(box1,null);
            alert(obj.width);
            //该方法会返回一个对象,对象中封装了当前元素对应的样式
            //可以通过对象.样式名来读取样式
            //如果获取的样式没有设置,则会返回真实的值,而不是默认值(比如auto?)
            ````
            3. 下面这个办法好像麻烦???
            ````js
            var currentStyle = function (element) {
                return element.currentStyle || document.defaultView.getComputedStyle(element, null);
            };
            alert(currentStyle(box1).width);
            ````
    3. 正常浏览器的方式
    ````js
    alert(getComputedStyle(box1.null).width);
    ````
    4. IE8及以下的方式(虽然我没有成功...)
    ````js
    alert(box1.currentStyle.width);
    //???鱼和熊掌不可兼得?上面那个和这个不能同时实现?
    //微软你事情怎么那么多???
    //活该IE没人乐意用!?(好吧我还要用)
    ````
    5. 好吧那就自己上
* 通过getComputedStyle和currentStyle读取到的样式都是只读的,不能修改
* 如果要修改必须通过style属性
# 其他样式相关的属性
![](2021-06-15-15-47-45.png)
![](2021-03-29-08-11-20.png)
### clientWidth
### clientHeight
* 这两个属性可以获得元素的可见宽度和高度
* 返回值包括padding(可见宽度和高度,包括内容区和页边距)
* 不包括border和margin
* 不能修改原数值,只读
![](2021-03-29-08-24-08.png)
### offsetWidth
### offsetHeight
* 可以获取元素整个的大小
* 包括padding和border
* 不能修改原数值,只读
![](2021-03-29-08-28-08.png)
### offsetParent
* 可以获得当前元素的定位父元素
* 会获取到离当前元素最近的开启定位的祖先元素
* 如果所有元素都没有开启定位,则返回body
![](2021-03-31-16-46-57.png)
### offsetLeft
* 当前元素相对于其定位元素的水平偏移量
### offsetTop
* 当前元素相对于其定位元素的垂直偏移量
PS:其定位元素即offsetParent返回的元素
![](2021-03-31-16-47-11.png)
### scrollHeight
### scrollWidth
* 滚动宽度,滚动高度
* 可以获得元素整个滚动区域的高度或宽度
![](2021-03-31-16-46-36.png)
### scrollLeft
* 可以获得水平滚动条滚动的距离
### scrollTop
* 可以获得垂直滚动条滚动的距离
* 当满足scrollHeight - scrollTop == clientHeight时,说明垂直滚动条滚动到底了
* 当满足scrollWidth - scrollLeft == clientWidth时,说明水平滚动条滚动到底了
![](2021-03-31-17-18-29.png)
### onscroll
* 该元素会在元素的滚动条滚动时触发
![](2021-03-31-17-37-34.png)
### disabled
* 可以设置一个元素是否禁用
* true 禁用
* false 不禁用
![](2021-03-31-17-38-19.png)
# 事件对象
![](2021-04-01-15-04-05.png)
# div随鼠标移动
* onmousemove是干啥用的
### clientX和clientY
* 用于获取鼠标在当前的可见窗口的坐标
* div的偏移量是相对于整个页面的
### pageX和pageY
* 可以获取鼠标相对于当前页面的坐标
* 这两个属性在IE8中不支持
* 如果需要兼容IE8则无法使用
# 事件的冒泡
### 事件的冒泡(Bubble)
* 所谓的冒泡指的是事件的向上传导,当后代元素上的事件被触发时,其祖先元素的事件时间也会被触发
* 在开发中,大部分冒泡是有用的
* 如果不希望发生事件冒泡,可以通过事件对象取消冒泡
    - event.cancelBubble = true;
    - 取消冒泡
# 事件的委派
* 指将事件统一绑定给元素共同的祖先元素,这样当后代元素上的事件触发时,会一直冒泡到祖先元素
* 从而通过祖先元素的响应函数来处理事件
* 事件的委派利用了冒泡,通过委派可以减少事件绑定的次数,提高程序的性能
### target 
* 返回触发此事件的元素
````js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        window.onload = function(){
            var u1 = document.getElementById("u1");
            var btn01 = document.getElementById("btn01");
            btn01.onclick = function(){
                // alert("添加一个超链接")
                // 创建一个li
                var li = document.createElement("li");
                li.innerHTML = "<a class='link' href='javascript:;'>新建的超链接</a>";
                // 将li添加到ul中
                // 
                u1.appendChild(li); 
            }
            /*
             * 为每一个超链接都绑定一个单机响应函数
             * 我们希望,只绑定一次事件,即可应用到多个元素上,即使元素是后添加的
             * 可以尝试将其绑定给元素共同的祖先元素
             * 
             * 事件的委派
             *  - 只包含一个class,多个的话就不行了
             *  - 指将事件统一绑定给元素共同的祖先元素,这样当后代元素上的事件触发时,会一直冒泡到祖先元素
             *  - 从而通过祖先元素的响应函数来处理事件
             *  - 事件的委派利用了冒泡,通过委派可以减少事件绑定的次数,提高程序的性能
             */ 
            // 获取所有a
            var allA = document.getElementsByTagName("a");
            // 遍历
            // for(var i = 0;i < allA.length;i++){
            //     allA[i].onclick = function(){
            //         alert("我是a的单击响应函数");
            //     };
            // }
            u1.onclick = function(){
                // 如果触发事件的对象是我们期望的元素,则执行,否则不执行
                // alert("我是ul的单击响应函数");
                // alert(this);
                /*
                 * target
                 *  - event中的target表示的触发时间的对象
                 */ 
                event = event || window.event;
                // alert(event.target);
                if(event.target.className == "link"){
                    alert("我是ul的单击响应函数");
                }
            }
        };
    </script>
</head>
<body>
    <button id="btn01">添加超链接</button>
    <ul id="u1">
        <li><a class="link" href="javascript:;">超链接一</a></li>
        <li><a class="link" href="javascript:;">超链接二</a></li>
        <li><a class="link" href="javascript:;">超链接三</a></li>
    </ul>
</body>
</html>
````
## 事件的委派
* 只包含一个class,多个的话就不行了
* 指将事件统一绑定给元素共同的祖先元素,这样当后代元素上的事件触发时,会一直冒泡到祖先元素
* 从而通过祖先元素的响应函数来处理事件
* 事件的委派利用了冒泡,通过委派可以减少事件绑定的次数,提高程序的性能
# 事件的绑定
* 点击按钮以后弹出一个内容
* 使用 对象.事件 = 函数 的形式绑定响应函数
* 它只能同时为一个元素的一个事件绑定一个响应函数
* 不能绑定多个,如果绑定了多个,则后面的会覆盖掉前面的
### addEventListener
* 通过这个方法也可以为元素绑定响应函数
* 当时间被触发时,响应函数将会按照函数的绑定顺序执行
* 使用这个方法可以同时为一个元素的相同事件同时绑定多个响应函数
* 这样当事件被触发时,响应函数会按照函数的绑定顺序执行 
* 参数
    1. 时间的字符,不要on
    2. 回调函数,当事件触发时该函数会被调用
    3. 是否在捕获阶段触发事件,一般都传false
    ````js
    btn01.addEventListener("click",function(){
        alert(1);
    },false);
    btn01.addEventListener("click",function(){
        alert(2);
    },false);
    btn01.addEventListener("click",function(){
        alert(3);
    },false);
    btn01.attachEvent();
    ````
### attachEvent()
* 在IE8中可以使用attachEvent来绑定事件
* 只能用于IE8以下
* 这个方法也可以为一个事件绑定多个处理函数
* 不同的是它是后绑定先执行
* 执行顺序和addEventListener()相反
* 参数(只有两个):
    1. 事件的字符串,需要加on
    2. 回调函数
    ````js
    btn01.attachEvent("onclick",function(){
        alert(3);
    });
    btn01.attachEvent("onclick",function(){
        alert(2);
    });
    btn01.attachEvent("onclick",function(){
        alert(1);
    });
    ````
* 定义一个函数,用来为指定元素绑定函数
* addEventListener()中的this是绑定事件的对象
* attachEvent()中的this是window
* 需要统一一两个方法中的this
* this由调用方式决定
* callback.call(obj)
    1. 浏览器调用匿名函数
    2. 在匿名函数里面调用回调函数
* 参数:
    1. obj 要绑定事件的对象
    2. eventStr 事件的字符串(不要on)
    3. callback 回调函数
````js
function bind(obj,eventStr,callback){
````js
function bind(obj,eventStr,callback){
if(addEventListener){
    // 大部分浏览器兼容的方式
    obj.addEventListener(eventStr,callback,false)
}
else{
    // IE8及以下
    // this是谁由调用方式决定
    
    // 浏览器调用匿名函数
    obj.attachEvent("on" + eventStr,function(){
        // 在匿名函数里面调用回调函数
        // callback();
        callback.call(obj)
    });
}
````                                                                                                                     
# 事件的传播
* 关于事件的传播,网景公司和微软公司有不同的理解
* 微软公司:认为事件应该是由内向外传播的
* 也就是当事件触发时,应该先触发当前元素上的事件
* 然后再向当前元素的祖先元素上传播
* 也就是说事件应该在冒泡阶段执行
* 网景公司:事件应该是由外向内传播的
* 也就是说当前事件触发时,应该先触发当前元素的最外层祖先元素的事件,
* 然后再向内传播给后代元素
* 最后由W3C决定,综合了两个公司的方案,将事件的传播分成了三个阶段
    1. 捕获阶段
        - 在捕获阶段时从最外层的祖先元素向目标元素进行事件的捕获,但是默认此时不会触发事件
    2. 目标阶段
        - 事件捕获目标元素,捕获结束开始在目标元素上触发事件
    3. 冒泡阶段
        - 时间从目标元素向它的祖先元素传递,依次触发祖先元素上的事件
* 如果希望在捕获阶段就触发事件,可以将addEventListener()的第三个参数设置为true
* 一般情况下我们不会希望在捕获阶段触发事件,所以这个参数一般都是false
* IE8及以下的浏览器没有捕获阶段
````js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #box1{
            width: 300px;
            height: 300px;
            background-color: aquamarine;
        }
        #box2{
            width: 200px;
            height: 200px;
            background-color: cornflowerblue;
        }
        #box3{
            width: 150px;
            height: 150px;
            background-color: mediumorchid;
        }
    </style>
    <script>
        window.onload = function(){
            // 分别为3个div绑定单机响应函数
            var box1 = document.getElementById("box1");
            var box2 = document.getElementById("box2");
            var box3 = document.getElementById("box3");
            /*
             * 事件的传播
             * 关于事件的传播,网景公司和微软公司有不同的理解
             * 微软公司:认为事件应该是由内向外传播的
             * 也就是当事件触发时,应该先触发当前元素上的事件
             * 然后再向当前元素的祖先元素上传播
             * 也就是说事件应该在冒泡阶段执行
             * 网景公司:事件应该是由外向内传播的
             * 也就是说当前事件触发时,应该先触发当前元素的最外层祖先元素的事件,
             * 然后再向内传播给后代元素
             * 最后由W3C决定,综合了两个公司的方案,将事件的传播分成了三个阶段
             * 1. 捕获阶段
             * - 在捕获阶段时从最外层的祖先元素向目标元素进行事件的捕获,但是默认此时不会触发事件
             * 2. 目标阶段
             * - 事件捕获目标元素,捕获结束开始在目标元素上触发事件
             * 3. 冒泡阶段
             * - 时间从目标元素向它的祖先元素传递,依次触发祖先元素上的事件
             * - 如果希望在捕获阶段就触发事件,可以将addEventListener()的第三个参数设置为true
             * 一般情况下我们不会希望在捕获阶段触发事件,所以这个参数一般都是false
             * IE8及以下的浏览器没有捕获阶段
             */ 
            bind(box1,"click",function(){
                alert("我是box1的响应函数");
            });
            bind(box2,"click",function(){
                alert("我是box2的响应函数");
            });
            bind(box3,"click",function(){
                alert("我是box3的响应函数");
            });
        };
        function bind(obj,eventStr,callback){
            if(obj.addEventListener){
                // 大部分浏览器兼容的方式
                obj.addEventListener(eventStr,callback,true);
            }
            else{
                // IE8及以下的兼容方式
                obj.attachEvent("on" + eventStr,function(){
                    callback.call(obj);
                });
            }
        }
        /*function bind(obj,eventStr,callback){
            if(obj.addEventListener){
                // 大部分浏览器兼容的方式
                obj.addEventListener(eventStr,callback,false);
            }
            else{
                // IE8及以下的兼容方式
                obj.attachEvent("on" + eventStr,function(){
                    callback.call(obj);
                });
            }
        }*/
    </script>
</head>
<body>
    <div id="box1">
        <div id="box2">
            <div id="box3"></div>
        </div>
    </div>
</body>
</html>
````

# 拖拽
![](2021-04-05-14-36-46.png)

![](2021-04-05-15-43-28.png)
````js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #box1{
            width: 100px;
            height: 100px;
            background-color: aquamarine;
            position: absolute;
        }
        #box2{
            width: 100px;
            height: 100px;
            background-color: cornflowerblue;
            position: absolute;
            left: 200px;
            top: 200px;
        }
    </style>
    <script>
        window.onload = function(){
            /*
             * 拖拽box1元素
             * 拖拽的流程
             * 1. 当鼠标在被拖拽元素上按下时,开始拖拽 onmousedown
             * 2. 当鼠标移动时被拖拽元素跟随鼠标移动 onmousemove
             * 3. 当鼠标松开时,被拖拽元素固定在当前位置 onmouseup
             */ 
            var box1 = document.getElementById("box1");
            var box2 = document.getElementById("box2");
            // 为box1绑定一个鼠标按下事件
            // 当鼠标在被拖拽元素上按下时,开始拖拽 onmousedown
            box1.onmousedown = function(event){
                // 设置box1捕获所有鼠标按下的事件
                /*if(box1.setCapture){
                    box1.setCapture();
                }*/
                box1.setCapture && box1.setCapture();
                // 如果前面为false(不存在此元素),就直接不看后面的了
                // 只有IE支持,但是在火狐中调用不会报错
                // 但是使用Chrome时会报错
                // alert("鼠标按下,开始拖拽");
                event = event || window.event;
                // 求出div的偏移量 
                // 鼠标.clientX - 元素.offsetLeft
                // 鼠标.clientY - 元素.offsetTop
                var ol = event.clientX - box1.offsetLeft;
                var ot = event.clientY - box1.offsetTop;
                // 当鼠标移动时被拖拽元素跟随鼠标移动 onmousemove
                document.onmousemove = function(event){
                    event = event || window.event;
                    // 当鼠标移动时,被拖拽元素跟随鼠标移动 onmousemove
                    // 获取鼠标坐标
                    // var left = event.clientX;
                    // var top = event.clientY;
                    var left = event.clientX - ol;
                    var top = event.clientY - ot;
                    // 修改box1的位置
                    box1.style.left = left + "px";
                    box1.style.top = top + "px";
                };
                // 当鼠标松开时,被拖拽元素固定在当前位置 onmouseup
                // 为元素绑定一个鼠标松开事件
                document.onmouseup = function(){
                    // 当鼠标松开时,取消对事件的捕获
                    // 所以...懵了...
                    box1.releaseCapture && box1.releaseCapture();
                    // 效果同上,自己去看!!!
                    // IE去死!!!
                    // 当鼠标松开时,被拖拽元素固定在当前位置 onmouseup
                    // 取消document的onmousemove事件
                    document.onmousemove = null;
                    // 取消document的onmouseup事件

                };
                /*
                 * 当我们拖拽一个页面中的内容时,浏览器会默认去搜索引擎中搜索内容
                 * 此时会导致拖拽功能的异常,这是浏览器提供的默认行为
                 * 如果不希望发生此行为,可以通过return false 来取消该行为
                 * 但是对IE8无效
                 */ 
                return false;
            };
            box2.onmousedown = function(event){
                // 设置box1捕获所有鼠标按下的事件
                /*if(box1.setCapture){
                    box1.setCapture();
                }*/
                box2.setCapture && box2.setCapture();
                // 如果前面为false(不存在此元素),就直接不看后面的了
                // 只有IE支持,但是在火狐中调用不会报错
                // 但是使用Chrome时会报错
                // alert("鼠标按下,开始拖拽");
                event = event || window.event;
                // 求出div的偏移量 
                // 鼠标.clientX - 元素.offsetLeft
                // 鼠标.clientY - 元素.offsetTop
                var ol = event.clientX - box2.offsetLeft;
                var ot = event.clientY - box2.offsetTop;
                // 当鼠标移动时被拖拽元素跟随鼠标移动 onmousemove
                document.onmousemove = function(event){
                    event = event || window.event;
                    // 当鼠标移动时,被拖拽元素跟随鼠标移动 onmousemove
                    // 获取鼠标坐标
                    // var left = event.clientX;
                    // var top = event.clientY;
                    var left = event.clientX - ol;
                    var top = event.clientY - ot;
                    // 修改box1的位置
                    box2.style.left = left + "px";
                    box2.style.top = top + "px";
                };
                // 当鼠标松开时,被拖拽元素固定在当前位置 onmouseup
                // 为元素绑定一个鼠标松开事件
                document.onmouseup = function(){
                    // 当鼠标松开时,取消对事件的捕获
                    // 所以...懵了...
                    box2.releaseCapture && box2.releaseCapture();
                    // 效果同上,自己去看!!!
                    // IE去死!!!
                    // 当鼠标松开时,被拖拽元素固定在当前位置 onmouseup
                    // 取消document的onmousemove事件
                    document.onmousemove = null;
                    // 取消document的onmouseup事件

                };
                /*
                 * 当我们拖拽一个页面中的内容时,浏览器会默认去搜索引擎中搜索内容
                 * 此时会导致拖拽功能的异常,这是浏览器提供的默认行为
                 * 如果不希望发生此行为,可以通过return false 来取消该行为
                 * 但是对IE8无效
                 */ 
                return false;
            };
        }
    </script>
</head>
<body>
    我是一段文字
    <div id="box1"></div>
    <div id="box2"></div>
</body>
</html>
````

````js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #box1{
            width: 100px;
            height: 100px;
            background-color: aquamarine;
            position: absolute;
        }
        #box2{
            width: 100px;
            height: 100px;
            background-color: cornflowerblue;
            position: absolute;
            left: 200px;
            top: 200px;
        }
    </style>
    <script>
        window.onload = function(){
            /*
             * 拖拽box1元素
             * 拖拽的流程
             * 1. 当鼠标在被拖拽元素上按下时,开始拖拽 onmousedown
             * 2. 当鼠标移动时被拖拽元素跟随鼠标移动 onmousemove
             * 3. 当鼠标松开时,被拖拽元素固定在当前位置 onmouseup
             */ 
            // 提取一个专门用来拖拽的函数
            // 参数:
            // 开启拖拽的元素
            var box1 = document.getElementById("box1");
            var box2 = document.getElementById("box2");
            var img1 = document.getElementById("img1");
            // 为box1绑定一个鼠标按下事件
            // 当鼠标在被拖拽元素上按下时,开始拖拽 onmousedown
            drag(box1);
            drag(box2);
            drag(img1);
        }
        function drag(obj){
            obj.onmousedown = function(event){
                // 设置box1捕获所有鼠标按下的事件
                /*if(box1.setCapture){
                    box1.setCapture();
                }*/
                obj.setCapture && obj.setCapture();
                // 如果前面为false(不存在此元素),就直接不看后面的了
                // 只有IE支持,但是在火狐中调用不会报错
                // 但是使用Chrome时会报错
                // alert("鼠标按下,开始拖拽");
                event = event || window.event;
                // 求出div的偏移量 
                // 鼠标.clientX - 元素.offsetLeft
                // 鼠标.clientY - 元素.offsetTop
                var ol = event.clientX - obj.offsetLeft;
                var ot = event.clientY - obj.offsetTop;
                // 当鼠标移动时被拖拽元素跟随鼠标移动 onmousemove
                document.onmousemove = function(event){
                    event = event || window.event;
                    // 当鼠标移动时,被拖拽元素跟随鼠标移动 onmousemove
                    // 获取鼠标坐标
                    // var left = event.clientX;
                    // var top = event.clientY;
                    var left = event.clientX - ol;
                    var top = event.clientY - ot;
                    // 修改box1的位置
                    obj.style.left = left + "px";
                    obj.style.top = top + "px";
                };
                // 当鼠标松开时,被拖拽元素固定在当前位置 onmouseup
                // 为元素绑定一个鼠标松开事件
                document.onmouseup = function(){
                    // 当鼠标松开时,取消对事件的捕获
                    // 所以...懵了...
                    obj.releaseCapture && obj.releaseCapture();
                    // 效果同上,自己去看!!!
                    // IE去死!!!
                    // 当鼠标松开时,被拖拽元素固定在当前位置 onmouseup
                    // 取消document的onmousemove事件
                    document.onmousemove = null;
                    // 取消document的onmouseup事件

                };  
            /*
            * 当我们拖拽一个页面中的内容时,浏览器会默认去搜索引擎中搜索内容
            * 此时会导致拖拽功能的异常,这是浏览器提供的默认行为
            * 如果不希望发生此行为,可以通过return false 来取消该行为
            * 但是对IE8无效
            */ 
                return false;
            };
        };
    </script>
</head>
<body>
    我是一段文字
    <div id="box1"></div>
    <div id="box2"></div>
    <img src="./img/13.png" id="img1" alt="" style="position: absolute;" width="250px" height="170px">
</body>
</html>
````

# 滚轮的事件
### onmousewheel
* 鼠标滚轮滚动事件,会在滚轮滚动时触发
* 但是火狐不支持该属性
* 在火狐中需要使用DOMMouseScroll来绑定滚动事件
* 该事件需要通过addEventListener()函数来绑定
### event.wheelDelta
* 可以获取鼠标滚轮滚动的方向
so...
* 当鼠标滚轮向下滚动时,box1变长
* 当滚轮向上滚动时,box1变短
* event.wheelDelta可以获取鼠标滚轮滚动的方向
* 向上滚是120
* 向下滚是-120
* event.wheelDelta不看大小只看正负
* event.wheelDelta在火狐(FireFox)中不支持
* 当滚轮滚动时，如果浏览器有滚动条，滚动条会随之滚动
* 这是浏览器的默认行为，如果不希望发生此行为则可以取消默认行为
* 使用addEventListener()方法绑定响应函数，取消默认行为时不能使用return false
* 需要使用event来取消默认行为
* 方法：event.preventDefault();
````js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #box1{
            width: 100px;
            height: 100px;
            background: url(./img/13.png);
        }
    </style>
    <script>
        window.onload = function(){
            /*
             * 当鼠标滚轮向下滚动时,box1变长
             * 当滚轮向上滚动时,bix1变短
             *
             */ 
            // 获取id为box1的div
            /*
             * onmousewheel
             * 鼠标滚轮滚动事件,会在滚轮滚动时触发
             * 但是火狐不支持该属性
             * 在火狐中需要使用DOMMouseScroll来绑定滚动事件
             * 该事件需要通过addEventListener()函数来绑定
             */ 
            var box1 = document.getElementById("box1");
            // 为box1绑定一个鼠标滚轮滚动的事件
            // function fun(){
                
            // };
            box1.onmousewheel = function(){
                // alert("滚了~");
                // 判断鼠标滚轮滚动的方向
                event = event || window.event;
                // alert(event.wheelDelta);
                // 好像除了IE其他的都是第一次怎么滚,以后后显示那个,所以???被捕获了?
                // (⊙﹏⊙)好像并不是
                if(event.wheelDelta > 0 || event.detail < 0){
                    // alert("向上滚~");
                    // 向上滚,box1变短
                    box1.style.height = box1.clientHeight - 10 + "px";
                }
                else{
                    // alert("向下滚~");
                    // 向下滚，box1变长
                    box1.style.height = box1.clientHeight + 10 + "px";
                }
                event.preventDefault && event.preventDefault();
                return false;
                // alert(event.detail);
                // 挨千刀的!!!为什么向上向下都是-3?!?!
                // 火狐你脑子怕是有坑
                // IE8:火狐，今天咱俩只能活一个
                /*
                 * 当鼠标滚轮向下滚动时,box1变长
                 * 当滚轮向上滚动时,box1变短
                 * event.wheelDelta可以获取鼠标滚轮滚动的方向
                 * 向上滚是120
                 * 向下滚是-120
                 * event.wheelDelta不看大小只看正负
                 * event.wheelDelta在火狐(FireFox)中不支持
                 * 当滚轮滚动时，如果浏览器有滚动条，滚动条会随之滚动
                 * 这是浏览器的默认行为，如果不希望发生此行为则可以取消默认行为
                 * 使用addEventListener()方法绑定响应函数，取消默认行为时不能使用return false
                 * 需要使用event来取消默认行为
                 * 方法：event.preventDefault();
                 */ 
            };
            // 作为回调函数传入
            bind(box1,"DOMMouseScroll",box1.onmousewheel);
        };
        // 121
        function bind(obj,eventStr,callback){
            if(obj.addEventListener){
                // 大部分浏览器兼容的方式
                obj.addEventListener(eventStr,callback,false)
            }
            else{
                // IE8及以下
                // this是谁由调用方式决定
                
                // 浏览器调用匿名函数
                obj.attachEvent("on" + eventStr,function(){
                    // 在匿名函数里面调用回调函数
                    // callback();
                    callback.call(obj)
                });
            }
            // if(!addEventListener){
            //     // IE8及以下
            //     // this是谁由调用方式决定
                
            //     // 浏览器调用匿名函数
            //     obj.attachEvent("on" + eventStr,function(){
            //         // 在匿名函数里面调用回调函数
            //         // callback();
            //         callback.call(obj)
            //     });
            // }
            // else{
            //     // 大部分浏览器兼容的方式
            //     obj.addEventListener(eventStr,callback,false)
            // }
        };
    </script>
</head>
<body style="height: 2000px;">
    <div id="box1"></div>
</body>
</html>
````

# 键盘事件
![](2021-04-05-21-38-03.png)

![](2021-04-05-22-00-03.png)

![](2021-04-05-22-00-51.png)

###  onkeydown
* 按键被按下
* 对于onkeydown来说，如果一直按下某个按键不松手，则事件一直在触发
* 当onkeydown连续触发时，第一次和第二次间隔的时间会稍微长一点，其他的都非常快
* 防止发生误操作，所以在第一次和第二次之间停留较长时间
### onkeyup
* 按键被松开
* 键盘事件一般都会绑定给一些可以获得焦点的对象或者是document
### keyCode
* 可以通过keyCode来获得按键的编码
* 可以判断哪个按键被按下
* console.log("按键被按下");
* console.log(event.keyCode);
* 除了keyCode,事件对象还提供了几个属性
* altKey
* ctrlKey
* shiftKey
* 这三个用来判断alt,ctrl和shift是否被按下
* 如果按下则返回true,否则返回false
````js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /* #box1{
            width: 100px;
            height: 100px;
            background-color: mediumslateblue;
        } */
    </style>
    <script>
        window.onload = function(){
            /*
             * 键盘事件
             * onkeydown
             *  - 按键被按下
             *  - 对于onkeydown来说，如果一直按下某个按键不松手，则事件一直在触发
             *  - 当onkeydown连续触发时，第一次和第二次间隔的时间会稍微长一点，其他的都非常快
             *  - 防止发生误操作，所以在第一次和第二次之间停留较长时间
             * onkeyup
             *  - 按键被松开
             * 键盘事件一般都会绑定给一些可以获得焦点的对象或者是document
             */ 
            document.onkeydown = function(event){
                event = event || window.event;
                // 可以通过keyCode来获得按键的编码
                // 可以判断哪个按键被按下
                // console.log("按键被按下");
                // console.log(event.keyCode);
                /*
                 * 除了keyCode,事件对象还提供了几个属性
                 * altKey
                 * ctrlKey
                 * shiftKey
                 * 这三个用来判断alt,ctrl和shift是否被按下
                 * 如果按下则返回true,否则返回false
                 * 
                 */ 
                if(event.keyCode === 89 && event.ctrlKey){
                    alert("Y和Ctrl都被按下");
                }
            }
            // document.onkeyup = function(){
            //     console.log("按键松开了");
            // }
            var input = document.getElementsByTagName("input")[0];
            input.onkeydown = function(event){

                // 使文本框中不能输入数字
                event = event || window.event;
                // 数字ASCII码48-57
                console.log(event.keyCode);
                if(event.keyCode >= 48 && event.keyCode <= 57 || event.keyCode >= 96 && event.keyCode <= 105){
                    return false;
                }
                // 在文本框中输入内容,属于onkeydown的默认行为
                // 如果在onkeydown中取消了默认行为,则输入的内容不会出现在文本框内
                // return false;
            }
        };
    </script>
</head>
<body>
    <input type="text" name="" id="">
</body>
</html>
````
## 键盘事件练习
````js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #box1{
            width: 250px;
            height: 170px;
            background-color: cornflowerblue;
            position: absolute;
        }
    </style>
    <script>
        // 使div可以根据不同的方向键向不同的方向移动
        /*
         * 按左键,向左移
         * 按右键,向右移
         * ...以此类推
         */ 
        window.onload = function(){
            // 虽然你可以但是为什么要把你定义到这里,还有我的var呢
            var box1 = document.getElementById("box1");
            // 为document绑定一个按键按下的事件
            document.onkeydown = function(event){
                event = event || window.event;
                // 定义一个变量表示移动的速度
                var speed = 10;
                // 当用户按下ctrl,速度加快
                // 哦豁,要一直按着
                if(event.ctrlKey){
                    speed = 500;
                }
                console.log(event.keyCode);
                /*
                 * 左 37 
                 * 上 38
                 * 右 39
                 * 下 40
                 */
                // 
                switch(event.keyCode){
                    case 37: 
                        // alert("向左");
                        box1.style.left = box1.offsetLeft - speed + "px";
                        break;
                    case 38: 
                        // alert("向上");
                        box1.style.top = box1.offsetTop - speed + "px";
                        break;
                    case 39: 
                        // alert("向右");
                        box1.style.left = box1.offsetLeft + speed + "px";
                        break;
                    case 40: 
                        // alert("向下");
                        box1.style.top = box1.offsetTop + speed + "px";
                        break;
                        
                }
            };
        };
    </script>
</head>
<body>
    <div id="box1">
        <img src="./img/13.png" alt="" width="250px" height="170px">
    </div>
</body>
</html>
````
# BOM
* 浏览器对象模型
* 可以使我们通过JS操作浏览器
* 在BOM中为我们提供了一组数据用来完成对浏览器的操作
### Window
* 代表整个浏览器窗口,同时也是网页中的全局对象
### Navigator 
![](2021-04-07-17-04-24.png)
* 代表当前浏览器的信息,通过该对象可以识别不同的浏览器
* 由于历史原因,Navigator中的大部分属性都不能帮我们识别不同的浏览器
* 一般只会使用userAgent 来判断浏览器的信息
* 比如:ActiveXObject(只有IE能显示,其他的都报错)
* 如果通过userAgent不能判断,还可以通过一些浏览器中特有的对象,来判断浏览器的信息
````js
var ua = navigator.userAgent;
if(/firefox/i.test(ua)){
    alert("你是火狐!");
}
else if(/chrome/i.test(ua)){
    alert("你是Chrome");
}
else if(/msie/i.test(ua)){
    alert("你是IE浏览器");
}
else if("ActiveXObject" in window){
    alert("IE11扑街啊!!!");
}
````
### Location
![](2021-04-08-14-25-34.png)

![](2021-04-08-14-27-11.png)
* 代表的是浏览器的地址栏信息,通过Location可以获取地址栏信息,或者操作浏览器跳转网页
### History
* 代表浏览器的历史记录,可以通过该对象来操作浏览器的历史记录
* 由于隐私原因,该对象不能获取到具体的历史记录,只能操作浏览器向前或向后翻页
* 而且该操作只在当次访问时有效
#### History
* 对象可以用来操作浏览器向前或向后翻页
##### length
* 可以获取当次访问链接的数量
##### back
* 可以用来回退到上一个页面,作用和浏览器的回退按钮一样
##### forward
* 可以跳转下一个页面,作用和浏览器的前进按钮一样
##### go
* 可以用来跳转到指定页面
* 它需要一个整数作为参数
* 1 表示向前跳转一个页面,相当于forward()
* 2 表示向前跳转两个页面
* -1 表示向后跳转一个页面
* -2 向后跳转两个页面
### Screen
* 代表用户屏幕的信息,通过该对象可以获得到用户显示器的相关的信息
* 这些DOM对象在浏览器中都是作为window对象的属性保存的
* 可以通过window对象来使用,也可以直接使用
![](2021-04-07-16-50-04.png)

# 定时器简介(定时调用)
![](2021-04-08-14-43-00.png)
![](2021-04-08-14-43-16.png)
* JS的程序的执行速度是非常快的
* 如果希望一段程序可以每间隔一段时间执行一次,可以使用定时调用
### setInterval()
* 定时调用
* 可以将一个函数每隔一段时间执行一次
* 参数:
    1. 回调函数,该函数会每隔一段时间调用一次
    2. 每次调用间隔的时间,单位是毫秒
* 返回值:返回一个number类型的数据,这个数字用来作为定时器的唯一标识
### clearInterval()
* 可以用来关闭一个计数器 
* 方法中需要一个定时器的标识作为参数,这样将关闭对应的定时器
* 可以接受任意参数,如果参数是一个有效的定时器表示,则停止对应的定时器
* 如果参数不是一个有效的标识,则什么也不做
````js
var count = document.getElementById("count");
var num = 1;
var timer = setInterval(function(){
    count.innerHTML = num++;
    if(num == 21){
        clearInterval(timer);
    }
},100);
````
* 目前,我们每点击一次按钮,就会开启一个定时器
* 点击多次就会开启多个计时器,这就导致图片切换速度加快
* 而我们只能关闭最后一个计时器
* 在开启定时器之前,需要将上一个关闭
![](2021-06-17-16-57-48.png)
![](2021-06-17-16-57-55.png)
````js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        window.onload = function(){
            var btn01 = document.getElementById("btn01");
            var btn02 = document.getElementById("btn02");
            // 使图片可以自动切换
            var img1 = document.getElementById("img1");
            // 创建一个数组保存图片路径
            var imgArr = ["./img/01.jpg","./img/02.jpg","./img/03.jpg","./img/04.jpg","./img/05.jpg","./img/06.jpg","./img/07.jpg","./img/08.jpg","./img/09.jpg","./img/10.jpg","./img/11.jpg","./img/12.jpg","./img/13.png"];
            // 创建一个变量,用来保存当前图片的索引
            var index = 0;
            // 定义一个变量,用来保存定时器的标识
            var timer;
            btn01.onclick = function(){
                /*
                 * 目前,我们每点击一次按钮,就会开启一个定时器
                 * 点击多次就会开启多个计时器,这就导致图片切换速度加快
                 * 而我们只能关闭最后一个计时器
                 * 在开启定时器之前,需要将上一个关闭
                 */ 
                clearInterval(timer);
                // 哦豁这方法绝了哈哈好厉害
                // 在开启定时器之前,需要将当前元素上的其他定时器关闭
                timer = setInterval(function(){
                    index++;
                    // 修改img的src属性
                    // 判断索引是否超过最大索引
                    /*if(index >= imgArr.length){
                        index = 0;
                    }*/
                    index = index % imgArr.length;
                    img1.src = imgArr[index];
                },1000);                
            };
            // 为btn02绑定单击响应函数
            btn02.onclick = function(){
                // 点击按钮后听停止图片自动切换
                clearInterval(timer);
                /*
                 * clearInterval()
                 * 可以接受任意参数,如果参数是一个有效的定时器表示,则停止对应的定时器
                 * 如果参数不是一个有效的标识,则什么也不做
                 */ 
            }
        }
    </script>
</head>
<body>
    <img id="img1" src="./img/01.jpg" alt="" width="500" height="300">
    <br>
    <br>
    <button id="btn01">开始</button>
    <button id="btn02">停止</button>
</body>
</html>
````
# 延时调用
* 演示调用一个函数不马上执行,而是隔一段时间以后再执行,而且只会执行1次
* 延时调用和定时调用的区别:
* 定时调用会执行多次,而延时调用只会执行一次
* 使用clearTimeout()来关闭延时调用
* 延时调用和定时调用实际上是可以相互代替的
* 在开发中可以根据自己的需要去选择
![](2021-04-14-18-50-00.png)
![](2021-04-14-18-50-16.png)
# 方法一:匿名函数自调
* 把 i 的作用域限定在匿名函数内，也就是变成局部变量，局部变量在执行完毕后，会自动释放
````js
for(var i=0;i<button.length;i++){
    (function (i) {
            button[i].onclick = function(){
            alert(i+1);
        }
})(i);
````
# 方法二:使用let
* let会把变量的作用域限定在当前代码块内
````js
for(let i = 0;i < button.length;i++){
    button[i].onclick = function(){
        alert(i+1);
    };
}
````
![](2021-04-17-21-55-03.png)
# 定时器的应用
* 在计时器函数中,为了防止多次点击按钮导致开启多个定时器,所以在每一次执行函数时都需要先关闭上一次开启的定时器
* 作用于不同的对象时,可以为每个对象定义一个定时器(obj.timer),防止多个对象定时器之间相互干扰
# 类的操作
* 通过style属性来修改元素的样式,每修改一个样式,浏览器就需要重新渲染一次页面
* 这样执行的性能是比较差的
* 修改多个样式时不太方便
* 希望一行代码同时修改多个样式
* 通过修改元素的class属性来间接的修改样式
* 这样一来,只需要修改一次即可同时修改多个样式
* 浏览器只需要重新渲染一次,性能比较好
* 并且这种方式可以使表现与行为进一步分离
- 修改box的class属性
- b2可以将b1共有的元素覆盖
- b2前面一定要加空格,否则会变成"b1b2"
- "b1 b2"
- 类并集用空格隔开
````js
box.className += " b2";
````
````js
// 判断一个元素中是否含有指定的class值
/*  
    * 参数
    * obj 要添加class属性的元素
    * cn 要添加的class值
    * 如果没有该class值,返回false
    * 如果有该class,则返回true
*/ 
// ? 好像主要还是这个不太懂,先记下
function hasClass(obj,cn){
    // 判断obj里面有没有cn class
    // 采用正则表达式
    // \b 单词边界
    // var reg = /\bb2\b/;
    // 不能写死,要构造函数
    // 字符串中\\ = \
    // 动态生成正则表达式

    var reg = new RegExp("\\b"+cn+"\\b");
    // 正则表达式的检索功能
    // alert(reg);
    return reg.test(obj.className);
}
// 定义一个函数,用来向一个元素中添加指定的class属性
/*
 * 参数
 * obj 要添加class属性的元素
 * cn 要添加的class值
 */ 
function addClass(obj,cn){
    if(!hasClass(obj,cn)){
        obj.className += " "+cn;
    }
}
/*
    * 删除元素中指定的一个class属性
    * 参数
    * obj 要删除class属性的元素
    * cn 要删除的class值
    */ 
function removeClass(obj,cn){
    // 创建一个正则表达式
    var reg = new RegExp("\\b"+cn+"\\b");
    // 删除class
    obj.className = obj.className.replace(reg,"");
}
/*
    * toggleClass 切换
    * 可以用来切换一个类
    * 如果元素中具有该类,则删除,如果没有则添加
    */ 
function toggleClass(obj,cn){
    // 判断obj中是否含有该class
    if(hasClass(obj,cn)){
        removeClass(obj,cn);
    }
    else{
        addClass(obj,cn);
    }
}
````
# JSON
* JSON在IE7及以下浏览器不支持
* JavaScript Object Notation
* JS中的对象只有JS认识,其他语言都不认识
* JSON就是一个特殊格式的字符串,这个字符串可以被任意语言识别
* 并且可以转换成任意语言的对象
* JSON在开发中主要用于数据的交互
* JSON和JS对象格式一样,只不过JSON字符串中属性名必须加双引号
* 一旦写成JSON,属性名必须加双引号,整体加单引号
* 其他的和JS语法一致
* JSON分类
1. JSON对象{}
2. JSON数组[]
* JSON中允许的值
1. 字符串
2. 数值
3. 布尔值
4. null
5. 对象(普通对象,不能是函数对象)
6. 数组
````js
var obj = '{"name":"Looking","age":20,"gender":"女"}';
var arr = '[1,2,3,"hello",true]';
var obj2 = '{"arr":[1,2,3]}';
var arr2 = '[{"name":"Looking","age":20,"gender":"女"},{"name":"Looking","age":20,"gender":"女"}]';
````
* 将JSON中的字符串转化成JS中的对象
* 在JS中,为我们提供了一个工具类,就叫JSON
* 这个对象可以帮助我们将一个JSON转化成JS对象,也可以将JS对象转化成JSON
* JSON --> JS对象
## JSON.parse();
* 可以将JSON字符串转化成JS对象
* 它需要一个JSON字符串作为参数,会将其转化成JS对象并返回
````js
var json = '{"name":"Looking","age":20,"gender":"女"}';
var o = JSON.parse(json);
var arr = '[1,2,3,"hello",true]';
var o2 = JSON.parse(arr);
````
* JS对象 --> JSON
## JSON.stringify();
* 可以将一个JS对象转化成JSON字符串
* 需要一个js对象作为参数,会返回一个JSON字符串
````js
var obj3 = {name:"Fris",age:19,gender:"女"};
var o3 = JSON.stringify(obj3);
console.log(typeof o3);
console.log(o3);
````
## eval();
* 这个函数可以用来执行一段字符串形式的代码,并将执行结果返回
* 如果eval()执行的字符串中含有{},会将{}当作是代码块
* 如果不希望被当成代码块解析,则需要在字符串前后各添加一个代码块
* eval()函数功能很强大,可以直接执行一个字符串中的JS代码
* 但是在开发中尽量不要使用
* 1. 执行性能比较差
* 2. 还具有安全隐患
````js
var str2 = "alert('Hello');";
eval(str2);
var str = '{"name":"Looking","age":20,"gender":"女"}';
var obj = eval("("+str+")");
console.log(obj);
````
* 如果需要兼容IE7及以下浏览器的JS的操作,
* 可以直接通过引入一个外部JS文件来处理
