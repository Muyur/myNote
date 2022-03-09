## PureComponent和Component的区别

二者的区别 :

- ​	`PureComponent`通过`prop`和`state`的浅比较来实现`shouldComponentUpdate`,当`prop`或`state`的值或者引用地址发生改变时,组件就会进行更新
- 而`Component`只要`state`发生改变,不论值是否与之前的相等,都会触发更新

浅比较的概念

对比**当前状态(current)**和**下一个状态(next)**下`prop`和`state`时,比较基本数据类型是否相等(例如: `'a' === 'a'`),而引用数据类型则是比较其引用地址是否相同,与值无关

> 注意：在 `PureComponent` 中，当对传入的对象或者数组进行直接赋值时，因为并没有改变其引用地址，所以就不引起重新渲染。









































