# Setstate()

## setState()的使用

1. `setState(updater,[callback])`

   `updater`为返回`stateChange`对象的函数: `(state,props) => stateChange`

   接收的`state`和`props`被保证为最新的

2. `setState(stateChange,[callback])`

   `setState`为对象

   `callback`是可选的回调函数,在状态更新且页面更新后才执行

3. 总结

   对象方式是函数方式的简写方式

   ​	如果新状态不依赖于原状态 ==> 使用对象方式

   ​	如果新状态依赖于原状态 ==> 使用函数方式

   如果需要在`setState()`后获取最新的状态数据,在第二个`callback`函数中读取

## setState()的异步与同步

1. `setState()`更新状态是异步还是同步的?

   - 执行`setState()`的位置?

     在`react`控制的回调函数中: 生命周期钩子 / `react`事件监听回调

     非`react`控制的异步回调函数中: 定时器回调 / 原生事件监听回调 / `promise`回调 / ...

   - 异步 or 同步?

     `react`相关回调中: 异步

     其他异步回调中: 同步

2. 关于异步的`setState()`

   - 多次调用,如何处理?

     `setState({})`: 合并更新一次状态,只调用一次`render()`更新界面 --> 状态更新和页面更新都合并了

     `setState(fn)`: 更新多次状态,但只调用一次`render()`更新界面 --> 状态更新没有合并,但界面更新合并了

   - 如何得到异步更新后的状态数据

     在`setState()`的`callback`回调函数中

## Component与PureComponent

1. `Component`存在的问题

   - 父组件重新`render()`,当前组件也会重新执行`render()`,即使没有发生任何变化
   - 当前组件`setState()`,重新执行`rend()`,及时`state`没有任何变化

2. 解决`Component`存在的问题

   - 原因: 组件的`componentShouldUpdate()`,默认返回`true`,及时没有数据变化`render()`也会重新执行
   - 办法1: 重写`shouldComponentUpdate()`,判断如果有数据变化,返回`true`,否则返回`false`
   - 方法2: 使用`PureComponent`代替`Component`
   - 说明: 一般都使用`PureComponent`来优化组件性能

3. `PureComponent`的基本原理

   - 重写实现`shouldComponentUpdate()`
   - 对组件的新/旧`state`和`props`中的数据进行浅比较,如果都没有变化,就返回`false`,否则返回`true`
   - 一旦`componentShouldUpdate()`返回`false`,不再执行用于更新的`render()`

4. 面试题:

   组件的哪个生命周期钩子能实现组件优化

   PureComponent的原理?

   区别`Component`与`PureComponent`?

   







































