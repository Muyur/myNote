# React

React 是一个将数据渲染为 HTML 视图的开源 JavaScript 库

* 为什么要学 React

  1. 原生 JavaScript 操作 DOM 繁琐 , 效率低 (**DOM-API 操作 UI**)
  2. 使用 JavaScript 直接操作 DOM , 浏览器会进行**大量重绘重排**

  3. 原生 JavaScript 没有**组件化**编码方案 , 代码复用率低

* React 的特点
  1. 采用**组件化模式** , **声明式编码** , 提高开发效率及组件复用率
  2. 在 React Native 中可以使用 React 语法进行**移动端开发**
  3. 使用**虚拟 DOM** + 优秀的 **Diffing 算法** , 尽量减少与真实 DOM 的交互

* React 官网
  * 中文官网 : https://react.docschina.org/
  * 英文官网 : https://reactjs.org/

### 虚拟 DOM 

#### 关于虚拟 DOM

1. 本质是 Object 类型的对象 (一般对象)
2. 虚拟 DOM 比较"轻" (属性比较少) , 真实 DOM 比较 "重"(所含属性多) , 因为虚拟 DOM 是 React 内部在用 , 无需真实 DOM 上那么多属性
3. 虚拟 DOM 最终会被 React 转化成真实 DOM

#### jsx 语法规则

* JSX 全称 JavaScriptXML
* react 定义的一种类似于 XML 的 JS 拓展语法 : JS + XML
* 语法规则 :
  * 定义虚拟 DOM 时 , 不要写引号

  * 标签中混入 JS 表达式时 , 要使用 { }

    > 区分 JS 语句(代码) 与 JS 表达式
    >
    > 1. 表达式 : 一个表达式会产生一个值 , 可以放在任何一个需要值的地方
    >
    >    下面的这些都是表达式
    >
    >    - a
    >    - a + b
    >    - demo(1) 
    >    - arr.map( )
    >    - function test( ){ }
    >
    > 2. 语句(代码)
    >
    >    下面这些都是语句(代码)
    >
    >    * if( ){ }
    >    * for( ){ }
    >    * switch( ){case:xxx}

  * 央视的类名指定不要用 class , 要用 className

  * 内联样式 , 要用 `style={{key:value}}` 的形式去写

  * 虚拟 DOM 必须只有一个根标签

  * 标签必须闭合

  * 标签首字母

    * 若是小写字母开头 , 则将该标签转为 html 标签 , 如果 html 重没有该标签 , 则报错
    * 若大写字母开头 , React 就去渲染对应的组件 , 若组件没有定义 , 则报错

### React 面向组件编程

#### 函数式定义组件

````js
// 创建函数式组件
function MyComponent(){
    // 此处的this是指undefined,因为babel编译后开启了严格模式
    console.log(this);
    return <h2>我是函数定义的组件(适用于[简单组件]的定义)</h2>
}
// 渲染组件到页面
ReactDOM.render(<MyComponent/>,document.getElementById('test'));
````

执行了 `ReactDOM.render(<MyComponent/>,document.getElementById('test'));`代码之后发生了什么

1. React解析组件标签,找到了MyComponent组件
2. 发现组件时使用函数定义的,随后调用该函数,将返回的虚拟DOM转为真实DOM,随后呈现在页面中

#### 类的基本知识

1. 类中的构造不是必须写的,要对实例进行一些初始化操作,如添加指定属性时才写
2. 如果A类继承了B类,且A类中写了构造器,那么A类构造器中的`super`是必须调用的
3. 类中所定义的方法,都是放在了类的原型对象上,供实例去使用

#### 类式组件

````js
// 创建类式组件
class MyComponent extends React.Component{
    render(){
        // render是放在哪里的 ——类的原型对象上,供实例使用
        // render中的this是 ? MyComponent的实例对象上,MyComponent组件实例对象
        //MyComponent {props: {…}, context: {…}, refs: {…}, updater: {…}, _reactInternalFiber: FiberNode, …}
        return <h2>我是类定义的组件(适用于[复杂组件]的定义)</h2>
    }
}
// 2. 渲染组件到页面
ReactDOM.render(<MyComponent/>,document.getElementById('test'));
````

执行了`ReactDOM.render(<MyComponent/>,document.getElementById('test'))`之后,发生了什么?
1. React解析组件标签,找到了`MyComponent`组件
2. 发现组件是使用类定义的,随后`new`出来该类的实例,并通过该实例调用到原型上的`render`方法
3. 将render返回的虚拟DOM转为真实DOM,随后呈现在页面上

#### 组件实例的三大属性

>  constructor的作用
>
> * 通过给 `this.state` 赋值对象来初始化[内部 state](https://zh-hans.reactjs.org/docs/state-and-lifecycle.html)。
> * 为[事件处理函数](https://zh-hans.reactjs.org/docs/handling-events.html)绑定实例

##### state

* 状态 (`state`) 不可直接更改 , 要借助一个内置的 API 去更改(`setState`) 

````js
// 创建组件
class Weather extends React.Component{
    // 初始化状态
    state = {isHot:true}
    render(){
        const {isHot} = this.state
        return <h1 onClick={this.changeWeather}>今天天气很{isHot?'炎热':'凉爽'}</h1>
    }
    /**
     *% 箭头函数的this没有指向,会向外部找上一级的this
     *% 自定义方法 -- 要用赋值语句的形式+箭头函数
    */
    changeWeather = () => {
        const  isHot = this.state.isHot;
        this.setState({isHot:!isHot})
    }
}
// 渲染组件到页面
ReactDOM.render(<Weather/>,document.getElementById('test'));
````

##### props

* 如果想要对标签的属性进行类型 , 必要性限制 , 则需要引入`prop-type` 文件
* 如果不传参 , 就指定默认值

````react
// 创建组件
class Person extends React.Component{
    render(){
        const {name,age,gender} = this.props;
        // props是只读的
        return (
            <ul>
                <li>姓名:{name}</li>
                <li>年龄:{age+1}</li>   
                <li>性别:{gender}</li>
            </ul>
        )
    }
}
/** 
 *^ 对标签属性进行类型,必要性限制
 *^ 需要引入prop-type文件
 */
Person.propTypes = {
    name:PropTypes.string.isRequired,// 限制姓名为字符串且必传
    age:PropTypes.number,// 限制年龄为数字
    gender:PropTypes.string,// 限制性别为字符串
    // 函数类型比较特殊,JS中含有function关键字
    // 所以这里改用func
    speak:PropTypes.func // 限制speak为函数
}
/** 
 *^ 如果不传参,就指定默认值
 */
Person.defaultProps = {
    gender:'男',
    age:18
}
ReactDOM.render(<Person name='Tom' age={18} gender='男' speak={speak} />,document.getElementById('test1'));
ReactDOM.render(<Person name='Jerry' age={19} gender='男' />,document.getElementById('test2'));
const p1 = {name:'Ann',age:16,gender:'女'}
ReactDOM.render(<Person {...p1} />,document.getElementById('test3'));
speak = function(){
    console.log('我说话了');
}
````

简写

````react
        // 创建组件
        class Person extends React.Component{
            constructor(props){
                console.log(props);
                super(props)
            }
            /**
             *^ 加了static就可以放在对象里面 
            */
            static propTypes = {
                name:PropTypes.string.isRequired,// 限制姓名为字符串且必传
                age:PropTypes.number,// 限制年龄为数字
                gender:PropTypes.string,// 限制性别为字符串
            }
            static defaultProps = {
                gender:'男',
                age:18
            }
            render(){
                const {name,age,gender} = this.props;
                // props是只读的
                return (
                    <ul>
                        <li>姓名:{name}</li>
                        <li>年龄:{age+1}</li>   
                        <li>性别:{gender}</li>
                    </ul>
                )
            }
        }
        ReactDOM.render(<Person name='Tom' age={18} gender='男' />,document.getElementById('test'));
````

> **构造器是否接受props,是否传递给super,取决于:是否希望在构造器中通过this访问props**

* 通过标签数字那个从组件外向组件内传递变化的数据
* **注意 :** 组件内部不要修改 `props` 数据 (`props`数据是只读的)

##### refs

> 所以就是,直接给它赋一个ref属性,然后他们就都会被存储到this.refs里面
>
> 而且是以对象的形式
>
> 所以说,执行函数之类的,需要的时候就直接从this.refs里面取就OK了
>
> 但是test这个盒子就不能用
>
> 因为实例对象是放在test里面的,读取不到外面这个
>
> 失去焦点是onblur,记住了
>
> 原型中的函数必须放在render()上面吗?
>
> 添加的属性是ref而不是refs,但是最后ref的集合是refs

* 最简单的字符串方法

  > 但是现在已经不适用了

  ````react
  class Demo extends React.Component{
      showData1 = ()=>{
          // alert(this.refs.input1.value);
          const {input1} = this.refs;
          alert(input1.value)
      }
      showData2 = ()=>{
          // 所以这个可以只拿需要的数据喽
          const {input2} = this.refs;
          alert(input2.value)
      }
      /**
       * ^ refs上存储的是有ref属性的标签
      */
      render() {
          return (
              <div>
                  <input ref="input1" type="text" placeholder="点击按钮提示数据"/>&nbsp;
                  <button onClick={this.showData1}>点我提示左侧数据</button>&nbsp;
                  <input ref="input2" onBlur={this.showData2} type="text" placeholder="失去焦点提示数据"/>
              </div>
          )
      }
  }
  // 渲染组件到页面
  ReactDOM.render(<Demo/>,document.getElementById('test'));
  ````

* 箭头函数方法(是有点麻烦)

  > refs上存储的是有ref属性的标签
  >
  > 如果使用箭头函数的形式,currentNode指向的就是调用ref属性的标签
  >
  > 使用箭头函数的话 , 直接从实例对象身上取就行

  ````react
      class Demo extends React.Component{
          showData1 = ()=>{
              // alert(this.refs.input1.value);
              // const {input1} = this.refs;
              /**
               *^ 使用箭头函数的话
               *^ 直接从实例对象身上取就行
              */
              const {input1} = this;
              alert(input1.value)
          }
          showData2 = ()=>{
              // 所以这个可以只拿需要的数据喽
              // const {input2} = this.refs;
              const {input2} = this;
              alert(input2.value)
          }
          /**
           * ^ refs上存储的是有ref属性的标签
           * ^ 如果使用箭头函数的形式,currentNode指向的就是调用ref属性的标签
          */
          render() {
              return (
                  <div>
                      <input ref={(currentNode)=>{this.input1=currentNode}} type="text" placeholder="点击按钮提示数据"/>&nbsp;
                      <button onClick={this.showData1}>点我提示左侧数据</button>&nbsp;
                      <input ref={(currentNode)=>{this.input2=currentNode}} onBlur={this.showData2} type="text" placeholder="失去焦点提示数据"/>
                  </div>
              )
          }
      }
      // 渲染组件到页面
      ReactDOM.render(<Demo/>,document.getElementById('test'));
  /**
   * ^ 每次调用render,在更新的过程中回调(refs)都会被执行两次
   * ^ 在每次渲染时会创建一个新的函数实例，所以 React 清空旧的 ref 并且设置新的
   * ^ 过将 ref 的回调函数定义成 class 的绑定函数的方式可以避免上述问题
   * ^ 将函数放在实例自身
   * ^ 二者有区别但是无关紧要
  */
  ````

* 还有一种方法

  ````js
  class Demo extends React.Component{
      /**
       * ^ React.createRef调用之后可以返回一个容器,该容器可以存储被ref所标识后的节点
       * ^ 但是该容器是"专人专用"的,每个容器只能存一个
      */
      myRef = React.createRef();
      myRef2 = React.createRef();
      showData1 = ()=>{
          // const {input1} = this;
          // alert(input1.value)
          // console.log(this.myRef.current.value);
          alert(this.myRef.current.value)
      }
      showData2 = ()=>{
          // 所以这个可以只拿需要的数据喽
          // const {input2} = this.refs;
          // const {input2} = this;
          // alert(input2.value)
          alert(this.myRef2.current.value)
      }
      render() {
          return (
              <div>
                  <input ref={this.myRef} type="text" placeholder="点击按钮提示数据"/>&nbsp;
                  <button onClick={this.showData1}>点我提示左侧数据</button>
                  <input ref={this.myRef2} onBlur={this.showData2} type="text" placeholder="失去焦点提示数据"/>
              </div>
          )
      }
  }
  // 渲染组件到页面
  ReactDOM.render(<Demo/>,document.getElementById('test'));
  ````

> state上面存储数据,通过setState修改数据
> props的数据是只读的,可以引入prop-type文件,来对标签属性进行限制propTypes/defeultProps
> propTypes 对类型进行限制
> defeultProps 设置属性默认值

#### React 事件处理

1. 通过onXxx属性指定事件处理函数(注意大小写)
   * React使用的是自定义(合成)事件, 而不是使用的原生DOM事件 ———— 为了更好的兼容性
   * React中的事件是通过事件委托方式处理的(委托给组件最外层的元素) ———— 为了更加高效
2. 通过event.target得到发生事件的DOM元素对 ———— 不要过度使用ref

````react
        class Demo extends React.Component{
            /**
             * ^ React.createRef调用之后可以返回一个容器,该容器可以存储被ref所标识后的节点
             * ^ 但是该容器是"专人专用"的,每个容器只能存一个
            */
            // 创建ref容器
            /**
             *^  1.	通过onXxx属性指定事件处理函数(注意大小写)
             *^      1)	React使用的是自定义(合成)事件, 而不是使用的原生DOM事件 ———— 为了更好的兼容性
             *^      2)	React中的事件是通过事件委托方式处理的(委托给组件最外层的元素) ———— 为了更加高效
             *^  2.	通过event.target得到发生事件的DOM元素对 ———— 不要过度使用ref
            */
            myRef = React.createRef();
            myRef2 = React.createRef();
            showData1 = ()=>{
                // const {input1} = this;
                // alert(input1.value)
                // console.log(this.myRef.current.value);
                alert(this.myRef.current.value)
            }
            showData2 = (event)=>{
                // 所以这个可以只拿需要的数据喽
                // const {input2} = this.refs;
                // const {input2} = this;
                // alert(input2.value)
                // alert(this.myRef2.current.value)
                alert(event.target.value)
            }
            render() {
                return (
                    <div>
                        <input ref={this.myRef} type="text" placeholder="点击按钮提示数据"/>&nbsp;
                        <button onClick={this.showData1}>点我提示左侧数据</button>
                        <input onBlur={this.showData2} type="text" placeholder="失去焦点提示数据"/>
                    </div>
                )
            }
        }
        // 渲染组件到页面
        ReactDOM.render(<Demo/>,document.getElementById('test'));
````

#### React 收集表单数据

##### 非受控组件

````react
// 创建组件
class Login extends React.Component {
    handleSubmit = (event) => {
        // 阻止默认事件
        // 现用现取
        event.preventDefault();
        const {username,password} = this;
        alert(`你输入的用户名是${username.value},你输入的密码是${password.value}`);
    }
    render() {
        return (
            /**
             * ^ onSubmit 当表单提交的时候
             * ^ 表单提交是一个默认事件
             * ^ 如果不想引起页面刷新或者跳转就阻止默认事件
            */
            <form onSubmit={this.handleSubmit} actions="http://www.baidu.com">
                账号: <input ref={(c)=>{this.username=c}} type="text" name="username" />
                <br /><br />
                密码: <input ref={(c)=>{this.password=c}} type="password" name="password" />
                <br /><br />
                <button>登录</button>
            </form>
        )
    }
}
// 渲染组件到页面
ReactDOM.render(<Login />, document.getElementById('test'));
````

##### 受控组件

````react
// 创建组件
class Login extends React.Component {
    // 初始化状态
    // PS:我还是更喜欢Vue
    state = {
        username:'',
        password:''
    }
    /**
     * ^ 好像,相当于vue的双向绑定
    */
    saveUsername = () => {
        // console.log(event.target.value);
        // 每次表单数据发生变化就会引起state内数据的变化
        this.setState({username:event.target.value});
    }
    savePassword = () => {
        this.setState({password:event.target.value})
    }
    handleSubmit = (event) => {
        // 阻止默认事件
        // 现用现去
        event.preventDefault();
        const {username,password} = this.state;
        alert(`你输入的用户名是${username},你输入的密码是${password}`)
        // const {username,password} = this;
        // alert(`你输入的用户名是${username.value},你输入的密码是${password.value}`);
    }
    render() {
        return (
            /**
             * ^ onSubmit 当表单提交的时候
             * ^ 表单提交是一个默认事件
             * ^ 如果不想引起页面刷新或者跳转就阻止默认事件
            */
            <form onSubmit={this.handleSubmit} actions="http://www.baidu.com">
                账号: <input onChange={this.saveUsername} type="text" name="username" />
                <br /><br />
                密码: <input onChange={this.savePassword} type="password" name="password" />
                <br /><br />
                <button>登录</button>
            </form>
        )
    }
}
// 渲染组件到页面
ReactDOM.render(<Login />, document.getElementById('test'));
````

#### 高阶函数_函数的柯里化

> 高阶函数:如果一个函数符合下面2个规范中的任何一个,那该函数就是高阶函数
>
> 1. 若A函数,接收的参数是一个B函数,那A就可以称为高阶函数
>
> 2. 若A函数,调用的返回值依然是一个函数,那么A函数就可以称之为高阶函数
> 3. 常见的高阶函数 : Promise , setTimeout , arr.map()等等
>
> 函数的柯里化:通过函数调用继续返回函数的方式,实现多次接收参数最后统一处理的函数编码形式

````react
// 创建组件
class Login extends React.Component {
    state = {
        username:'',
        password:''
    }
    // 根据传入的数据的dataType来判断哪个更新

    saveFormData = (dataType) => {
        // 回调函数(?)
         /**
         * ^ return返回的也是一个函数
         * ^ 事件(onChange)的回调必须是一个函数
         * ^ 而saveFormData()的返回值就是一个函数
         * ^ 事件会自己帮忙调用函数,如果函数返回的不是function
         * ^ 那么事件就不能写函数后面的括号()
         */
        return ()=>{
            // console.log(dataType,event.target.value);
            this.setState({[dataType]:event.target.value});
        }
    }
    handleSubmit = (event) => {
        // 阻止默认事件
        // 现用现去
        event.preventDefault();
        const {username,password} = this.state;
        alert(`你输入的用户名是${username},你输入的密码是${password}`)
    }
    /**
     * ^ this.saveFormData('username') 是 saveFormData的回调函数,即return函数
     * ^ 必须把一个函数作为事件的回调
    */
    render() {
        return (
            <form onSubmit={this.handleSubmit} actions="http://www.baidu.com">
                账号: <input onChange={this.saveFormData('username')} type="text" name="username" />
                <br /><br />
                密码: <input onChange={this.saveFormData('password')} type="password" name="password" />
                <br /><br />
                <button>登录</button>
            </form>
        )
    }
}
// 渲染组件到页面
ReactDOM.render(<Login />, document.getElementById('test'));
````

* 函数柯里化举例

  ````js
  function sum(a){
      return (b)=>{
          return (c)=>{
              return a+b+c;
          }
      }
  }
  const result = sum(1)(2)(3);
  console.log(result);
  ````

#### 组件的生命周期

* `ReactDOM.unmountComponentAtNode(document.getElementById('test'))` 从某个容器内卸载组件
* `componentWillMount(){}` 组件将要挂载之前调用
* `componentDidMount(){}` 组件被挂载完毕之后调用
* `componentWillUnmount(){}` 组件被卸载之前调用
* 生命周期先调还是后调跟写的顺序没关系 

````js
/**
 * ^ render调用的时机:初始化渲染,状态更新之后
 * ^ componentDidMount 组件被挂载完毕
 * ^ componentWillUnmount 组件卸载之前
 * ^ setInterval 定时调用
 * ^ setTimeOut 延时调用
 * ^ 生命周期回调函数 <===> 生命周期钩子函数 <===> 生命周期函数 <===> 生命周期钩子
*/
// 创建组件
class Life extends React.Component {
    // 设置透明度状态
    state = {opacity:1}
    death = () => {
        // 放在这里也可以
        // clearInterval(this.timer)
        // 卸载 组件 从 结点
        // 点明哪个容器内的组件(?)
        ReactDOM.unmountComponentAtNode(document.getElementById('test'))
    }
    // 组件被挂载完毕之后调用
    componentDidMount(){
        this.timer = setInterval(() => {
            let {opacity} = this.state;
            opacity -= 0.1;
            if(opacity <= 0) opacity = 1;
            // opacity:opacity 这种前后相同的可以简写
            this.setState({opacity}) 
        },200)
    }
    // 组件卸载之前
    componentWillUnmount(){
        clearInterval(this.timer);
    }
    render() {
        return (
            <div>
                <h2 style={{opacity:this.state.opacity}}>React学不会怎么办?</h2>
                <button onClick={this.death}>不活了</button>
            </div>
        )
    }
}
// 渲染组件到页面
// 把组件挂载到页面
ReactDOM.render(<Life />, document.getElementById('test'));
````

##### 生命周期流程图 (旧)

![image-20210905103608512](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210905103608512.png)

 

1. 初始化阶段: 由ReactDOM.render()触发---初次渲染

   * `constructor()`

   * `componentWillMount()`

   * `render()`

   * `componentDidMount()` **常用**

     > 一般在这个钩子中做一些初始化的是,例如,开启定时器,发送网络请求,订阅消息

2. 更新阶段: 由组件内部`this.setSate()`或父组件重新`render`触发

   * `shouldComponentUpdate()`
   * `componentWillUpdate()`

   * `render()`
   * `componentDidUpdate()`

3. 卸载组件: 由`ReactDOM.unmountComponentAtNode()`触发

   * `componentWillUnmount()`   **常用**

     > 一般在这个钩子里做一些收尾的事,例如关闭定时器,取消消息订阅等



##### 生命周期流程图 (新)

![image-20210905123825737](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210905123825737.png)

````react
/**
 *^ static getDerivedStateFromProps() 得到一个派生的props
    *^ 此方法适用于罕见的用例，即 state 的值在任何时候都取决于 props
    *^ 派生状态会导致代码冗余，并使组件难以维护
    *^ 如果和state中的值相同,就会覆盖state中的值
    *^ getSnapshotBeforeUpdate 在更新之前获取快照
*/
// 创建组件
class Count extends React.Component {
    constructor(props) {
        console.log('Count-constructor');
        super(props)
    }
    state = { count: 0 }
    add = () => {
        let { count } = this.state;
        this.setState({ count: count + 1 })
    }
    // 卸载组件的方法
    death = () => {
        ReactDOM.unmountComponentAtNode(document.getElementById('test'));
    }
    // 不改变任何状态中的数据,强制更新
    force = () => {
        this.forceUpdate();
    }
    // getDerivedStateFromProps() 得到一个派生的props
    // 如果和state中的值相同,就会覆盖state中的值
    static getDerivedStateFromProps(props,state){
        console.log('getDerivedStateFromProps',props,state);
        // return props;
        return null;
    }
    // 组件挂载之后的钩子
    componentDidMount() {
        console.log('componentDidMount');
    }
    // 组件卸载之前
    componentWillUnmount() {
        console.log('componentWillUnmount');
    }
    // 组件是否应该被更新
    // 控制组件更新的阀门
    shouldComponentUpdate() {
        console.log('shouldComponentUpdate');
        return true
    }
    // 在更新之前获取快照
    /**
     * ! 更新之后页面上之前的数据就没有了
     * ! 但是有时候我们可能需要用到之前的数据
     * ! getSnapshotBeforeUpdate中的快照值可以用来保存之前的数据
     * ! 更新之前的数据,避免用到
    */
    getSnapshotBeforeUpdate(){
        console.log('getSnapshotBeforeUpdate');
        // return null;
        return 'React'
    }
    // 组件更新完毕的钩子
    /**
     * ^ 第一个参数:先前的props值
     * ^ 第二个参数:先前的state值
     * ^ 第三个参数:快照值
    */
    componentDidUpdate(preProps,prePState,snapshotValue) {
        console.log('componentDidUpdate',preProps,prePState,snapshotValue);
    }
    render() {
        console.log('render');
        const { count } = this.state
        return (
            <div>
                <h1>当前求和为:{count}</h1>
                <button onClick={this.add}>点我加1</button>
                <button onClick={this.death}>不活了</button>
                <button onClick={this.force}>强制更新</button>
            </div>
        )
    }
}
// 挂载组件到页面
ReactDOM.render(<Count count={100} />, document.getElementById('test'))
````

1. **初始化阶段:** 由`ReactDOM.render()`触发---初次渲染

   * `constructor()`
   * **`getDerivedStateFromProps `**
   *  `render()`

   * `componentDidMount() `  **常用**

     > 一般在这个钩子中做一些初始化的是,例如,开启定时器,发送网络请求,订阅消息

2. **更新阶段:** 由组件内部`this.setSate()`或父组件重新render触发

   * **`getDerivedStateFromProps`**

     > `getDerivedStateFromProps() `得到一个派生的props
     >
     > 此方法适用于罕见的用例，即 state 的值在任何时候都取决于 props
     > 派生状态会导致代码冗余，并使组件难以维护
     > 如果和state中的值相同,就会覆盖state中的值

   * `shouldComponentUpdate()`

   * `render()`

   * **`getSnapshotBeforeUpdate`**

     > `getSnapshotBeforeUpdate` 在更新之前获取快照

   * `componentDidUpdate()`

3. **卸载组件:** 由`ReactDOM.unmountComponentAtNode()`触发

   * `componentWillUnmount()`   **常用**

     > 一般在这个钩子里做一些收尾的事,例如关闭定时器,取消消息订阅等

> 详细介绍在代码中

##### 重要的勾子

1. `render`：初始化渲染或更新渲染调用

2. `componentDidMount`：开启监听, 发送ajax请求

3. `componentWillUnmount`：做一些收尾工作, 如: 清理定时器

##### 即将废弃的勾子

1. `componentWillMount`

2. `componentWillReceiveProps`

3. `componentWillUpdate`

> 如果要使用,需要在前面加`UNSAFE_` 
>
> 即 `UNSAFE_componentWillMount` 等

#### DOM的Diffing算法

##### key的使用(经典面试题)

> 经典面试题
> 1). React/Vue中的key有什么作用?(key的内部原理是什么?)
> 2). 为什么遍历列表时,key最好不要用index?

1. 虚拟DOM中key的作用:
   1. 简单地说:key是虚拟DOM对象的标识,在更新显示时key起着极其重要的作用
   2. 详细的说:当状态中的数据发生变化时,react会根据[新数据]生成[新的虚拟DOM],随后React进行[新虚拟DOM]与[旧虚拟DOM]的diff比较,比较规则如下:
       a. 旧虚拟DOM中找到了与新虚拟DOM相同的key
           (1). 旧虚拟DOM中内容没变,直接使用之前的真实DOM
           (2). 若虚拟DOM中内容变了,则生成新的真实DOM,随后替换掉页面中之前的真实DOM
       b. 旧虚拟DOM中未找到与新虚拟DOM相同的key
            根据数据创建新的虚拟DOM,随后渲染到页面
   3. 用index作为key可能会引发的问题
   4. 若对数据进行:你需添加,逆序删除等破坏顺序的操作
           会产生没有必要的真实DOM更新 ==> 页面效果没问题,但效率低 
   5. 如果结构中还包含输入类的DOM:
           会产生错误DOM更新 ==> 界面有问题	
   6. 注意:如果不存在对数据的你需添加,逆序删除等破坏顺序操作,仅用于渲染列表用于展示,使用index作为key是没有问题的
3. 开发中如何选择key?
           1) 最好使用每条数据的唯一标识作为key,比如id,手机号,身份证号,学号等唯一值
           2) 如果确定只是简单的展示数据,用index也是可以的

#### React todo 实例

##### uuid

> 专门生成唯一的id的库 (但是这个库占的内存比较大)

##### nanoid

> 占用内存较小 , 专门生成唯一的id值

##### PropType

> React脚手架搭建的项目没有自带prop-type的库,需要自己添加 : `yarn add prop-type `

##### 总结

1. 拆分组件 , 实现静态组件 , 注意 : `class Name` , `style` 的写法

2. 动态初始化列表 , 如何确定将数据放在哪个组件的`state` 中 ?
   * 某个组件使用 : 放在其自身的 `state` 中
   * 某些组件使用 : 放在他们共同的父组件的`state`中 (官方称为:**状态提升**)
   
3. 关于父子组件间通信 :
   * [父组件] 给 [子组件] 传递数据 : 通过 `props` 传递
   * [子组件] 给 [父组件] 传递数据 : 通过 `props` 传递 , 要求父提前给子传递一个函数
   
4. 注意`defaultChecked` 和 `checked` 的区别 , 类似的还有 `defaultValue` 和 `value`

   `defaultChecked` 一上来默认是否勾选的默认值,后续可以改 , `checked`后续不可以改,但是有了`onChange`就可以改

5. 状态在哪里 , 操作状态的方法就在哪里

#### axios

* 安装`axios` : `yarn add axios`

#### react脚手架配置代理总结

##### 方法一

> 在package.json中追加如下配置

```json
"proxy":"http://localhost:5000"
```

说明：

1. 优点：配置简单，前端请求资源时可以不加任何前缀。
2. 缺点：不能配置多个代理。
3. 工作方式：上述方式配置代理，当请求了3000不存在的资源时，那么该请求会转发给5000 （优先匹配前端资源）

##### 方法二

1. 第一步：创建代理配置文件

   ```
   在src下创建配置文件：src/setupProxy.js
   ```

2. 编写setupProxy.js配置具体代理规则：

   ```js
   const proxy = require('http-proxy-middleware')
   
   module.exports = function(app) {
     app.use(
       proxy('/api1', {  //api1是需要转发的请求(所有带有/api1前缀的请求都会转发给5000)
         target: 'http://localhost:5000', //配置转发目标地址(能返回数据的服务器地址)
         changeOrigin: true, //控制服务器接收到的请求头中host字段的值
         /*
         	changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
         	changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:3000
         	changeOrigin默认值为false，但我们一般将changeOrigin值设为true
         */
         pathRewrite: {'^/api1': ''} //去除请求前缀，保证交给后台服务器的是正常请求地址(必须配置)
       }),
       proxy('/api2', { 
         target: 'http://localhost:5001',
         changeOrigin: true,
         pathRewrite: {'^/api2': ''}
       })
     )
   }
   ```

**说明：**

1. **优点：可以配置多个代理，可以灵活的控制请求是否走代理。**
2. **缺点：配置繁琐，前端请求资源时必须加前缀。**

#### 消息的订阅预发布

* 工具库 PubSubJS
* 下载 : `npm install pubsub-js --save` 或者 `yarn add pubsub-js`

* 引入工具库 : `import PubSub from 'pubsub-js'`

* 消息的订阅

  ```js
  PubSub.subscribe("newName",(mas,data)=>{
      
  })
  ```

* 消息的发布

  ```js
  PubSub.publish("newName",data);
  ```

#### fetch

* [官方文档](https://github.github.io/fetch/)
* [fetch与xhr](https://segmentfault.com/a/1190000003810652)

* 特点
  * `fetch` : 原生函数 , 不再使用xhr对象提交ajax请求
  * 老版本浏览器可能不支持

#### ES6小知识点

解构赋值 + 重命名

```js
let pbj = {a:{b:1}};
const {a} = obj; // 传统解构赋值
const {a:{b}} = obj; // 连续解构赋值
const {a:{b:value}}; // 连续解构赋值+重命名 
```

#### 路由

##### SPA的理解

1. 单页Web应用（single page web application，SPA）。

2. 整个应用只有**一个完整的页面**。

3. 点击页面中的链接**不会刷新**页面，只会做页面的**局部更新。**

4. 数据都需要通过ajax请求获取, 并在前端异步展现。

##### 路由的理解

1. **什么是路由?**

   * 一个路由就是一个映射关系`(key:value)`

   * key为路径, value可能是`function`或`component`
2. **路由分类**

   * 后端路由：

     * 理解： `value`是`function`, 用来处理客户端提交的请求。

     * 注册路由：` router.get(path, function(req, res))`

     * 工作过程：当node接收到一个请求时, 根据请求路径找到匹配的路由, 调用路由中的函数来处理请求, 返回响应数据

   * 前端路由：

     * 浏览器端路由，value是component，用于展示页面内容。
     * 注册路由: `<Route path="/test" component={Test}>`
     * 工作过程：当浏览器的`path`变为`/test`时, 当前路由组件就会变为Test组件
3. react-router-dom 的理解

   * react的一个插件库
   * 专门用来实现一个SPA 应用
   * 基于react的项目基本都会用到此库
   * 安装 : `yarn add react-router-dom`

##### 路由的基本使用

1. 明确好界面中的导航区,展示区

2. 导航区的a标签改为Link标签

   ```html
   <Link to="/xxx">Demo</Link>
   ```

3. 展示区写Route标签进行路径的匹配

   ```html
   <Route path="/xxx" component={Demo} />
   ```

4. `<App>`最外侧包裹了一个`<browserRouter>`或`<HashRouter>`

##### 路由组件与一般组件

1. 写法不同 :

   一般组件:`<Demo/>`

   路由组件: `<Route path="/demo" component={Demo} />`

2. 存放位置不同 :

   一般组件: components

   路由组件: pages

3. 接收到的props不同

   一般组件: 写组件标签时传递了什么 , 就能接收到什么

   路由组件: 接收到三个固定的属性

   ```
   {history: {…}, location: {…}, match: {…}, staticContext: undefined}
   history:
       go: ƒ go(n)
       goBack: ƒ goBack()
       goForward: ƒ goForward()
       push: ƒ push(path, state)
       replace: ƒ replace(path, state)
   location:
       pathname: "/home"
       search: ""
       state: undefined
   match:
       params: {}
       path: "/home"
       url: "/home"
   ```

##### NavLink 与 封装NavLink

1. `NavLink`可以实现路由链接的高亮 , 通过`activeClassName`指定样式名
2. 标签体内容是一个特殊的标签属性
3. 通过`this,props,children`可以获取标签体内容
4. 封装的`MyNavLink`放在components文件中

##### Switch的使用

1. 通常情况下 , path和component是一一对应关系
2. Switch可以提高匹配效率(单一匹配)

##### 解决多级路径刷新页面样式丢失的问题

1. `public/index,html` 中引入样式时不写`./`写`/`(常用)
2. `public/index,html` 中引入样式时不写`./`写`%PUBLIC_URL%` (常用,只适用于React脚手架)
3. 使用`HashRouter`

##### 路由的严格匹配与模糊匹配

1. 默认使用的是模糊匹配 (简单记 : [输入的路径] 必须包含[匹配的路径] , 且顺序要一致 )
2. 开启严格模式 : `<Poute exact={true} path="/about" component={About}/>`
3. 严格匹配不要随便开启 , 需要再开 , 有些时候开启会导致无法继续匹配二级路由

##### Redirect 的使用

1. 一般写在所有路由注册想的最下方 , 当所有的路由都无法匹配时 , 跳转到`Redirect`指定的路由

2. 具体编码 : 

   ```html
   <Switch>
   <Route path="/about" component={About} />
   <Route path="/home" component={Home} />
   <Redirect to="/about" />	
   </Switch>
   ```

   

##### 嵌套路由

1. 注册子路由是要写上父路由的Path值
2. 路由的匹配是按照注册路由的顺序进行的

##### 向路由组件传递参数

1. `params`参数

   路由链接(携带参数) : `<Link *to*={`/home/message/detail/${msgObj.id}/${msgObj.title}`}>详情</Link>`

   注册路由(声明接收) : `<Route path="/home/message/detail/:id/:title" component={Detail} />`

   接收参数 : `const {id,title} = this.props.match.params`

2. `search`参数

   路由链接(携带参数) : `<Link to={/home/message/detail/?id=${msgObj.id}&title=${msgObj.title}}>详情</Link>`

   注册路由(声明接收) : `<Route path="/home/message/detail" component={Detail} />` (无需声明接收)

   接收参数 :  `this.props.location.search`

   备注 : 获取到的`search`是`urlencoded`编码字符串 , 需要借助`querystring`解析

3. `state` 参数

   路由链接(携带参数) : `<Link to={{pathname:'/home/message/detail',state:{id:msgObj.id,title:msgObj.title}}}>{msgObj.title}</Link>`

   注册路由(声明接收) : `<Route path="/home/message/detail" component={Detail} />` (无需声明接收)

   接收参数 :  `this.props.location.state || {}`

   备注 : 刷新之后也可以保留住参数

##### 编程式路由导航

借助`this.props.history`对象上的API对操作路由跳转 , 前进 , 后退

- `this.props.history.push()`
- `this.props.history.replace()`
- `this.props.history.goBack()`
- `this.props.history.goForward()`
- `this.props.history,go()`

##### BrowserRouter与HashRouter的区别

1. 底层原理不一样 :

   `BrowserRouter`使用的是 H5 的`history API` , 不兼容 IE9 以下的版本

   `HashRouter`使用的是 URL 的哈希值

2. path 表现不一样

   `BrowserRouter`的路径中没有 # , 例如 : `localhost:3000/demo/text`

   `HashRouter`的路径中包含 # , 例如 : `localhost:3000/#/demo/text` (#后面的内容不会发送给服务器)

3. 刷新后对路由`state`参数的影响

   `BrowserRouter`没有任何影响 , 因为`state`保存在`history`对象中

   `HashRouter`刷新后会导致路由`state`参数的丢失

4. 备注 : `HashRouter`可以用于解决一些路径错误的相关问题



# Redux

Redux工作原理图

![redux原理图](D:\AFrontEnd\frontEnd\React\react全家桶资料\02_原理图\redux原理图.png)

#### 求和案例

1. 去除Count组件自身的状态

2. src下建立 :

   -src

   ​	-redux

   ​		-store.js

   ​		-count_reducer.js

3. store.js

   1. 引入redux中的createStore函数 , 创建一个store
   2. createStore调用时要传入一个为其服务的reducer
   3. 记得暴露store对象

4. count_reducer.js

   1. reducer的本质是一个函数 , 接收 preState , action , 返回加工后的状态
   2. reducer有两个作用 : 初始化状态 , 加工状态
   3. reducer第一次被调用时 , 时store自动触发的,传递的preState时undefined

5. 在index.js中检测store中转台的改变 , 一旦发生改变重新渲染`<App/>`

   备注 : redux只负责管理状态 , 至于状态的改变驱动着页面的展示 , 要靠我们自己写

6. 完整版新增文件

   1. count_action.js 专门用于创建action对象
   2. constant.js 防止容易由于编码疏忽写错action中的type

##### 异步action

向store传一个函数作为返回值

需要引入redux-thunk进行解析 , 安装方式 : `yarn add redux-thunk`

1. 明确 : 延迟的动作不想交给组件自身 , 想交给 action
2. 何时需要异步action : 想要对状态进行操作 , 但是具体的数据靠异步任务返回
3. 具体编码 : 
   1) `yarn add redux-thunk` ,并配置在store中
   2) 创建action的函数不再返回一般对象 , 而是一个函数 , 该函数中写异步任务
   3) 异步任务有结果后 , 分发一个同步的action去真正操作数据

4. 备注 : 异步action不是必须要写的 , 完全可以自己等异步任务的结果出来之后再去分发同步action

#### react-redux

![react-redux模型图](D:\AFrontEnd\frontEnd\React\react全家桶资料\02_原理图\react-redux模型图.png)



* `mapStateToProps`函数返回的是一个对象

  返回的对象中的`key`就作为传递给UI组件props的`key`

  `value`就作为传递给UI组件props的value

  `mapStateToProps`用于传递状态

* `mapDispatchToProps`函数返回的也是一个对象

  返回的对象中的`key`就作为传递给UI组件props的`key`

  `mapDispatchToProps`用于传递操作对象的方法

##### react-redux的基本使用

1. 明确两个概念

   * UI组件 : 不能使用任何redux的api , 只负责页面的呈现 , 交互等
   * 容器组件 : 负责和redux通信 , 将结果交给UI组件

2. 如何创建一个容器组件 : 靠react-redux的connect函数

   `connect(mapStateToProps,mapDispatchToProps)(UI组件)`

   * mapStateToProps : 映射状态 , 返回值是一个对象
   * mapDispatchToProps : 映射操作状态的方法 , 返回值是一个对象

3. 备注1 : 容器组件中的store是靠props传进去的 , 而不是在容器组件中直接引入的

4. 备注2 : mapDispatchToProp也可以是一个对象

##### react-redux优化

1. 容器组件和UI组件混成一个组件

2. 无需自己给容器组件传递store , 给`>App/>`包裹一个`<Provider store={store}>`即可

3. 使用了react-redux后也不用自己再监测redux中状态的改变了,容器组件可以自动完成这个工作

4. mapDispatchToProps也可以简单的写成一个对象

5. 一个组件要和redux"打交道"需要经历哪几步

   1. 定义好UI组件(不暴露)

   2. 引入connect生成一个容器组件,并暴露,写法如下

      ```js
      connect(
      	state => ({key:value}), // 映射状态
      	{key:xxxAction}  // 映射操作状态的方法
      )(UI组件)
      ```

##### react-redux数据共享

1. 定义一个Person组件 , 和Count组件通过redux共享数据
2. 为Person组件编写 : reducer , action , 配置constant常量
3. 重点:Person的reducer和Conut的reducer要使用combineReducers进行合并,合并后的总状态是一个对象
4. 交给store的是总reducer , 最后注意在组件中取出状态的时候 , 记得"取到位 "

##### 纯函数

1. 一类他别的函数,只要书同样的输入(实参),必定得到同样的输出
2. 必须遵守以下一些约束
   * 不得改写参数数据
   * 不会产生任何副作用
   * 不能调用Date.now()或者Math.random()等不纯的方法
3. redux的render函数必须是一个纯函数

##### react-redux开发者工具的使用

1. `yarn add redux-devtools-extension`

2. store中进行配置

   `import {composeWithDevTools} from 'redux-devtools-extension'`

   `export default createStore(allReducer,composeWithDevTools(applyMiddleware(thunk)));`

##### react-redux最终规范

1. 所有变量名字要规范,尽量触发对象的简写形式
2. reducer文件夹中,编写index.js专门用于汇总暴露所有的reducer

#### 项目打包

1. 执行 `npm run build`
2. 安装serve,快速搭建服务器 : `npm i serve -g`
3. 执行`serve build`

# 拓展

## 1. setState

### setState更新状态的2种写法

```
	(1). setState(stateChange, [callback])------对象式的setState
            1.stateChange为状态改变对象(该对象可以体现出状态的更改)
            2.callback是可选的回调函数, 它在状态更新完毕、界面也更新后(render调用后)才被调用
					
	(2). setState(updater, [callback])------函数式的setState
            1.updater为返回stateChange对象的函数。
            2.updater可以接收到state和props。
            4.callback是可选的回调函数, 它在状态更新、界面也更新后(render调用后)才被调用。
总结:
		1.对象式的setState是函数式的setState的简写方式(语法糖)
		2.使用原则：
				(1).如果新状态不依赖于原状态 ===> 使用对象方式
				(2).如果新状态依赖于原状态 ===> 使用函数方式
				(3).如果需要在setState()执行后获取最新的状态数据, 
					要在第二个callback函数中读取
```



------



## 2. lazyLoad

### 路由组件的lazyLoad

```js
	//1.通过React的lazy函数配合import()函数动态加载路由组件 ===> 路由组件代码会被分开打包
	const Login = lazy(()=>import('@/pages/Login'))
	
	//2.通过<Suspense>指定在加载得到路由打包文件前显示一个自定义loading界面
	<Suspense fallback={<h1>loading.....</h1>}>
        <Switch>
            <Route path="/xxx" component={Xxxx}/>
            <Redirect to="/login"/>
        </Switch>
    </Suspense>
```



------



## 3. Hooks

#### 1. React Hook/Hooks是什么?

```
(1). Hook是React 16.8.0版本增加的新特性/新语法
(2). 可以让你在函数组件中使用 state 以及其他的 React 特性
```

#### 2. 三个常用的Hook

```
(1). State Hook: React.useState()
(2). Effect Hook: React.useEffect()
(3). Ref Hook: React.useRef()
```

#### 3. State Hook

```
(1). State Hook让函数组件也可以有state状态, 并进行状态数据的读写操作
(2). 语法: const [xxx, setXxx] = React.useState(initValue)  
(3). useState()说明:
        参数: 第一次初始化指定的值在内部作缓存
        返回值: 包含2个元素的数组, 第1个为内部当前状态值, 第2个为更新状态值的函数
(4). setXxx()2种写法:
        setXxx(newValue): 参数为非函数值, 直接指定新的状态值, 内部用其覆盖原来的状态值
        setXxx(value => newValue): 参数为函数, 接收原本的状态值, 返回新的状态值, 内部用其覆盖原来的状态值
```

#### 4. Effect Hook

```
(1). Effect Hook 可以让你在函数组件中执行副作用操作(用于模拟类组件中的生命周期钩子)
(2). React中的副作用操作:
        发ajax请求数据获取
        设置订阅 / 启动定时器
        手动更改真实DOM
(3). 语法和说明: 
        useEffect(() => { 
          // 在此可以执行任何带副作用操作
          return () => { // 在组件卸载前执行
            // 在此做一些收尾工作, 比如清除定时器/取消订阅等
          }
        }, [stateValue]) // 如果指定的是[], 回调函数只会在第一次render()后执行
    
(4). 可以把 useEffect Hook 看做如下三个函数的组合
        componentDidMount()
        componentDidUpdate()
    	componentWillUnmount() 
```

#### 5. Ref Hook

```
(1). Ref Hook可以在函数组件中存储/查找组件内的标签或任意其它数据
(2). 语法: const refContainer = useRef()
(3). 作用:保存标签对象,功能与React.createRef()一样
```



------



## 4. Fragment

### 使用

	<Fragment><Fragment>
	<></>

### 作用

> 可以不用必须有一个真实的DOM根标签了



<hr/>

## 5. Context

### 理解

> 一种组件间通信方式, 常用于【祖组件】与【后代组件】间通信

### 使用

```js
1) 创建Context容器对象：
	const XxxContext = React.createContext()  
	
2) 渲染子组时，外面包裹xxxContext.Provider, 通过value属性给后代组件传递数据：
	<xxxContext.Provider value={数据}>
		子组件
    </xxxContext.Provider>
    
3) 后代组件读取数据：

	//第一种方式:仅适用于类组件 
	  static contextType = xxxContext  // 声明接收context
	  this.context // 读取context中的value数据
	  
	//第二种方式: 函数组件与类组件都可以
	  <xxxContext.Consumer>
	    {
	      value => ( // value就是context中的value数据
	        要显示的内容
	      )
	    }
	  </xxxContext.Consumer>
```

### 注意

	在应用开发中一般不用context, 一般都用它的封装react插件



<hr/>


## 6. 组件优化

### Component的2个问题 

> 1. 只要执行setState(),即使不改变状态数据, 组件也会重新render() ==> 效率低
>
> 2. 只当前组件重新render(), 就会自动重新render子组件，纵使子组件没有用到父组件的任何数据 ==> 效率低

### 效率高的做法

>  只有当组件的state或props数据发生改变时才重新render()

### 原因

>  Component中的shouldComponentUpdate()总是返回true

### 解决

	办法1: 
		重写shouldComponentUpdate()方法
		比较新旧state或props数据, 如果有变化才返回true, 如果没有返回false
	办法2:  
		使用PureComponent
		PureComponent重写了shouldComponentUpdate(), 只有state或props数据有变化才返回true
		注意: 
			只是进行state和props数据的浅比较, 如果只是数据对象内部数据变了, 返回false  
			不要直接修改state数据, 而是要产生新数据
	项目中一般使用PureComponent来优化



<hr/>


## 7. render props

### 如何向组件内部动态传入带内容的结构(标签)?

	Vue中: 
		使用slot技术, 也就是通过组件标签体传入结构  <A><B/></A>
	React中:
		使用children props: 通过组件标签体传入结构
		使用render props: 通过组件标签属性传入结构,而且可以携带数据，一般用render函数属性

### children props

	<A>
	  <B>xxxx</B>
	</A>
	{this.props.children}
	问题: 如果B组件需要A组件内的数据, ==> 做不到 

### render props

	<A render={(data) => <C data={data}></C>}></A>
	A组件: {this.props.render(内部state数据)}
	C组件: 读取A组件传入的数据显示 {this.props.data} 



<hr/>

## 8. 错误边界

#### 理解：

错误边界(Error boundary)：用来捕获后代组件错误，渲染出备用页面

#### 特点：

只能捕获后代组件生命周期产生的错误，不能捕获自己组件产生的错误和其他组件在合成事件、定时器中产生的错误

##### 使用方式：

getDerivedStateFromError配合componentDidCatch

```js
// 生命周期函数，一旦后台组件报错，就会触发
static getDerivedStateFromError(error) {
    console.log(error);
    // 在render之前触发
    // 返回新的state
    return {
        hasError: true,
    };
}

componentDidCatch(error, info) {
    // 统计页面的错误。发送请求发送到后台去
    console.log(error, info);
}
```

## 9. 组件通信方式总结

#### 组件间的关系：

- 父子组件
- 兄弟组件（非嵌套组件）
- 祖孙组件（跨级组件）

#### 几种通信方式：

		1.props：
			(1).children props
			(2).render props
		2.消息订阅-发布：
			pubs-sub、event等等
		3.集中式管理：
			redux、dva等等
		4.conText:
			生产者-消费者模式

#### 比较好的搭配方式：

		父子组件：props
		兄弟组件：消息订阅-发布、集中式管理
		祖孙组件(跨级组件)：消息订阅-发布、集中式管理、conText(开发用的少，封装插件用的多)

## react-virtualized

### 1. 基本使用

1. 安装: `yarn add react-virtualized`

2. 在项目入口文件`index.js`中导入样式文件(只导入一次即可)

3. 打开 [文档](https://github.com/bvaughn/react-virtualized/blob/master/docs/List.md) ,点击`List`组件,进入`List`的文档

   ```js
   import 'react-virtualized/style.css'
   ```

4. 翻到文档最底部,将示例代码拷贝到项目中

































































