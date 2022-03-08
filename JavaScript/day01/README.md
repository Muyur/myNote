# JavaScript字符串和数组的相互转换

## 数组转换为字符串

### join()

`join()` 方法可以把数组转换为字符串，不过它可以指定分隔符。在调用 `join()` 方法时，可以传递一个参数作为分隔符来连接每个元素。如果省略参数，默认使用逗号作为分隔符，这时与` toString() `方法转换操作效果相同。

```js
var arr = [1,2,3,4,5];
var str1 = arr.join('');
var str2 = arr.join('-');
var str3 = arr.join(' ᓚᘏᗢ ');
var str4 = arr.join();
console.log(str1); // 12345
console.log(str2); // 1-2-3-4-5
console.log(str3); // 1 ᓚᘏᗢ 2 ᓚᘏᗢ 3 ᓚᘏᗢ 4 ᓚᘏᗢ 5
console.log(str4); // 1,2,3,4,5
```

### toString()

​	`toString()`将所有元素转换成逗号连接的字符串	

```js
var arr1 = [1,2,3,4,5,6];
var arr2 = ['a','b','c'];
var str1 = arr1.toString();
var str2 = arr2.toString();
console.log(str1); // 返回'1,2,3,4,5,6'
console.log(str2); // 返回'a,b,c'
var arr3 = [1,[2,3],[4,5]],[6,[7,[8,9],0]]];  //定义多维数组
var str3 = arr3.toString();  //把数组转换为字符串
console.log(str3);  //返回字符串“1,2,3,4,5,6,7,8,9,0”
```

### toLocalString()

`toLocalString()`将数组转换成本地约定的字符串

`toLocalString() `方法与` toString() `方法用法基本相同，主要区别在于 `toLocalString() `方法能够使用用户所在地区特定的分隔符把生成的字符串连接起来，形成一个字符串。

```js
var arr = [1,2,3,4,5];  //定义数组
var str = arr.toLocaleString();  //把数组转换为本地字符串
console.log(str);  // 返回'1,2,3,4,5'
```

### 数组相加

```js
var arr1 = [1,2,3,4,5];
var arr2 = [6,7,8,9];
var str = arr1 + arr2;
console.log(str); // 1,2,3,4,56,7,8,9
```

## 字符串转换成数组

### Split()

```js
var str = "abcde";
var arr = str.split(''); // ["u", "i", "x", "d", "k"]
```

用特殊字符分割字符串

```js
var str = 'hello-world';
var arr = str.split('-');
console.log(arr); // ['hello', 'world']
```

### ES6结构运算符

```js
var str = 'abcde';
var arr = [...str];
console.log(arr); //['a', 'b', 'c', 'd', 'e']
```

### Array.from()

```js
var str = 'abcde';
var arr = Array.from(str);
console.log(arr); //['a', 'b', 'c', 'd', 'e']
```

### Object.assign()

不会产生纯数组

> `Object.assign` 方法只会拷贝源对象自身的并且可枚举的属性到目标对象。该方法使用源对象的[[Get]]和目标对象的[[Set]]，所以它会调用相关 getter 和 setter。因此，它分配属性，而不仅仅是复制或定义新的属性。如果合并源包含getter，这可能使其不适合将新属性合并到原型中。

```js
var str = 'abcde';
var arr = Object.assign([],str);
console.log(arr); //['a', 'b', 'c', 'd', 'e']
```

