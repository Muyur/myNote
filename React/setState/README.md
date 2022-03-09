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


   







































