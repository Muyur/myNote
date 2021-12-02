### Vue 介绍

#### 什么是 Vue.js

- Vue.js 是目前最火的框架之一 , React 是最流行的一个框架 (React 除了开发网站 , 还可以开发手机 App)
- Vue.js 是目前前端的**主流框架之一** , 和 Angular.js , React.js 一起 , 并成为前端三大主流框架
- Vue.js 是一套构建用户界面的框架 , **只关注视图层** , 它不仅容易上手 , 还便于与第三方库或者既有项目整合 (Vue 有配套的第三方类库 , 可以整合起来做大型项目的开发 , Vue 语法也是可以用于手机 App 开发的 , 需要借助于 Weex)
- 前端的主要工作 ? 主要负责 MVC 中 V 这一层 , 主要工作就是**和界面打交道 , 来制作前端页面效果**

#### 为什么要学流行框架

* 企业为了提高开发效率 : 在企业中 , 时间就是效率 , 效率就是金钱
* 提高开发效率的发展历程∶原生JS -> Jquery之类的类库 -> 前端模板引擎 -> Angular.js / Vue.js (帮我们减少不必要的 DOM 操作 , 提高渲染效率)
* 在Vue中，一个核心的概念，**就是让用户不再操作DOM元素**，解放了用户的双手，让程序员可以更多的时间去关注业务逻辑
  * 通过框架提供的指令 , 我们前端程序员只需要关心数据的业务逻辑 , 不再关心 DOM 是如何渲染的了
* 增强自己就业时候的竞争力
  * 人无我有，人有我优

#### 项目和库的区别

* 框架:是一套完整的解决方案;对项目的侵入性较大，项目如果需要更换框架，则需要重新架构整个项目。
  * node 中的 express 
* 库（插件）︰提供某一个小功能，对项目的侵入性较小，如果某个库无法完成某些需求，可以很容易切换到其它库实现需求
  * 从 jQuery 到 Zepto
  * 从 EJS 到 art-template

#### Node(后端)中的 MVC 与前端中的 MVVM 之间的区别

* MVC是后端的分层开发概念
* MVVM是前端视图层的概念，主要关注于视图层分离，也就是说 : MVVM把前端的视图层，分为了三部分Model , View , VM ViewModel
* 为什么有了MVC还要有MVVM

![MVVM](D:\!笔记\Vue\MVVM.png)

### Vue 简介

#### Vue 介绍与描述

* 动态构建用户界面的**渐进式** JavaScript 框架
* 作者 : 尤雨溪

#### Vue 的特点 *

1. 遵循 MVVM 模式
2. 编码简洁 , 体积小 , 运行效率高 , 适合 **移动 / PC 端** 开发
3. 它本身只关注 UI , 也可以引入其它第三方库开发项目

#### 与其他 JS 框架的关联 *

1. 解建 Angular 的**模板**和**数据绑定**技术
2. 借鉴 **React** 的组件化和虚拟 **DOM** 技术

#### Vue 是什么

* Vue 是一套用与**构建用户界面**的**渐进式** JavaScript 框架
  - Vue 可以自底向上逐层的应用
    - 简单应用 : 只需要一个轻量小巧的核心库
    - 复杂应用 : 可以引入各种各样的 Vue 插件

#### Vue 周边库 

1. vue-cli : vue 脚手架
2. vue-resource
3. axios
4. vue-router : 路由
5. vuex : 状态管理
6. element-ui : 基于 vue 的 UI 组件库 ( PC 端 )
7. . . .

#### Vue 的特点

1. 采用**组件化**模式 , 提高代码复用效率 , 且让代码更好维护

2. **声明式**编码 , 让编码人员无需直接操作 DOM , 提高开发效率

   ![image-20210728144259044](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210728144259044.png)

   ![image-20210728144316647](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210728144316647.png)



![image-20210728144415348](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210728144415348.png)

3. 使用**虚拟DOM** + 优秀的 **Diff 算法** , 尽量复用 DOM 结点

![image-20210728144826970](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210728144826970.png)

![image-20210728144934455](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210728144934455.png)

![image-20210728145112526](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210728145112526.png)

#### 学习 Vue 之前需要掌握哪些 JavaScript 基础知识呢

* ES6 语法规范
* ES6 模块化
* 包管理器
* 原型 , 原型链
* 数组常用方法
* axios
* promise
* . . .

#### Vue 官网

* [英文官网](https://vuejs.org)
* [中文官网](https://cn.vuejs.org)

### Vue 核心

#### 初识Vue :

1. 想让Vue工作,就必须创建一个Vue实例,且要传入一个配置对象

2. root容器里的代码依然符合html规范,只不过混入了了一些特殊的vue语法

3. root容器里的代码被称为[Vue模板]

````html
    <!-- 准备好一个容器 -->
    <div id="root">
        <h1>Hello,{{name}}</h1>
    </div> 
    <script>
        // 设置为 false 以阻止 vue 在启动时生成生产提示
        Vue.config.productionTip = false; 

        // 创建 vue 实例
        new Vue({
            // el:document.getElementById('root') 这种也可以
            // element
            el:'#root', // el 用于指定当前Vue实例为哪个容器服务,值通常为css选择器字符串
            /*
             * data 中用于存储数据,数据供el所指定的容器去使用
             * 值 我们暂时先写成一个对象
            */
            data:{
                name:'World'
            }
        });
    </script>
````

* 如果一个Vue实例接管了两个及以上的容器 , 那么它只作用于第一个容器
* 如果一个容器被多个Vue实例接管 , 只有第一个的接管有效 , 后面的都无法接管它 , 并且会报错
* 容器与实例是一一对应的
* 真实开发中只有一个 vue 实例 , 并且会配合着组件一起使用
* {{ xxx }} 中的 xxx 要写 js 表达式 , 且 xxx 可以自动读取到 data 中的所有属性
* 一旦 data 中的数据发生变化 , 那么页面中用到该数据的地方也会自动更新 
* 注意区分 : JS 表达式 和 JS 代码(语句)
  * 表达式 : 一个表达式会产生一个值 , 可以放在任何一个需要值的地方
    * a
    * a + b
    * demo(1)
    * x === y ? 'a' : 'b'
  * JS 代码(语句)
    * if( ){ }
    * for( ){ }

#### Vue 的模板语法

* `v-bind` (可以简写为`:`) 
* Vue 模板语法有 2 大类
  1. 插值语法 : 
     - 功能 : 用于解析**标签体内容**
     - 写法 : {{ xxx }} , xxx 是 JS 表达式 , 且可以直接读取到 data 中的所有属性
  2. 指令语法
     * 功能 : **用于解析标签 (包括 : 标签属性 , 标签体内容 , 绑定事件 . .** .)
     * 举例 : `v-bind:href="xxx"` 或 简写为 `:href="xxx"` , xxx 同样要写 JS 表达式
     * 备注 : vue 中有很多的指令 , 且形式都是 : `v-???` , 此处我们只是拿 `v-bind` 举例子

#### Vue 数据绑定

Vue 中有 2 种数据绑定的方式

1. **单向绑定 (`v-bind`)** : 数据只能从 data 流向页面
2. **双向绑定 (`v-model`)** : value 可以简写为 `v-model` , 因为 `v-model` 默认手机的就是 value 值

#### el 与 data 的两种写法

* el 的两种写法

  * new Vue时候配置 el 属性
  * 先创建 Vue 实例 , 随后再通过 vm.$mount(' #root ') 指定 el 的值

  ````javascript
  Vue.config.productionTip = false;
  var v = new Vue({
      // 如果 data 中写两个name,则取第一个name
      // 第一种方法
      // el:'#root',
      data:{
          name:'World'
      }
  })
  // 第二种
  // v.$mount('#root');
  setTimeout(() => {
      v.$mount('#root');
  },1000);
  ````

* data 的两种写法

  * 对象式

  * 函数式

    如果选择 : 目前哪种写法都可以 , 以后学习到组件时 , data 必须使用函数时 , 否则会报错

  ````js
  Vue.config.productionTip = false;
  var v = new Vue({
      // 如果 data 中写两个name,则取第一个name
      el:'#root',
      // data的第一种写法:对象式
      // data:{
      //     name:'World'
      // }
      // data的第二种方法:函数式
      // 函数是Vue帮我们调用的
      // 函数所指的this是Vue实例对象
      // 前提是该函数是普通函数
      // 箭头函数的this指向的是window
      data:function(){
          return{
              name:'World'
          }
      }
  })
  // data(){
  //     return{
  //         name:'World'
  //     }
  // }
  ````

* 一个重要的原则

  由 Vue 管理的函数 , 一定不要写箭头函数 , 一旦写了箭头函数 , this 就不再是 Vue 实例的

#### MVVM 模型

* M : 模型 (Model) : 对应 data 中的数据
* V : 视图 (View) : 模板
* VM : 视图模型 (ViewModel) : Vue 实例对象

![image-20210731092435855](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210731092435855.png)

![image-20210731095529144](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210731095529144.png)

**观察发现 :**   

1. data 中所有的属性 , 最后都出现在了 vm 身上
2. **vm 身上所有的属性** , 及 **Vue 原型上所有的属性** , 在 Vue 模板中都可以直接使用

#### 数据代理

> 通过一个对象代理另一个对象中属性的操作 ( 读 / 写 )

![image-20210731121440728](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210731121440728.png)

![image-20210731121500428](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210731121500428.png)

#### 事件处理

##### 事件的基本使用

1. 使用 `v-on:xxx` 或 `@xxx` 绑定事件 , 其中 xxx 是事件名
2. 事件的回调需要配置在 methods 对象中 , 最终会在 vm 上
3. methods 中配置的函数 , 不要用箭头函数 , 否则 this 就不是 vm 了
4. methods 中配置的函数 , 都是被 Vue 所管理的函数 , this 的指向是 vm 或 组件实例对象
5. `@click="demo"` 和 `@click="demo($event)"` 效果一样 , 但后者可以传参

##### Vue 中的事件修饰符

1. **`prevent` : 阻止默认事件 (常用)**
2. **`stop` : 阻止事件冒泡 (常用)**
3. **`once` : 事件只触发一次 (常用)**
4. `capture` : 使用事件的捕获模式
5. `self` : 只有 `event.target` 是当前操作的元素才触发事件
6. `passive` : 事件的默认行为立即执行 , 无需等待事件回调执行完毕

##### 键盘事件

1. Vue 中常用的按键别名
   * 回车 => Enter
   * 删除 => Delete (捕获"删除"和"退格"键)
   * 退出 => Esc
   * 空格 => space
   * 换行 => tab (特殊 , 必须配合 keydown 去使用)
   * 上 => up
   * 下 => down
   * 左 => left
   * 右 => right
2. Vue 未提供别名的案件 , 可以使用按键原始的 key 值去绑定 , 但注意要转为kebab-case(短横线命名)
3. 系统修饰键(用法特殊) : Ctrl , Alt , Shift , meta
   * 配合 keyup 使用 : 按下修饰键的同时 , 再按下其他键 , 随后释放其他键 , 事件才被触发
   * 配合 keydown 使用 : 正常触发事件
4. 也可以使用 keyCode 去指定具体的按键(不推荐)
5. Vue.config.keyCodes.自定义键名 = 键码 , 可以去定制按键别名

#### 计算属性

1. 定义 : 要用的属性不存在，要通过**已有属性**计算得来。
2. 原理 : 底层借助了`Objcet.defineproperty`方法提供的 `getter` 和 `setter`.
3. get函数什么时候执行?
   * 初次读取时会执行一次。
   * 当依赖的数据发生改变时会被再次调用。
4. 优势:与methods实现相比， 内部有缓存机制(复用)，效率更高，调试方便。
5. 备注:
   * 计算属性最终会出现在 vm 上， 直接读取使用即可。
   * 如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生
6. **计算属性中是无法开启异步任务来维护数据**

````html
<body>
    <!-- 准备一个容器 -->
    <div id="root">
        姓: <input type="text" v-model="firstName"> <br> <br>
        名: <input type="text" v-model="lastName"> <br> <br>
        全名: <span>{{fullName}}</span>
    </div> 
</body>
<script>
    /**
     *+  1.定义:要用的属性不存在，要通过已有属性计算得来。
     *+  2.原理:底层借助了Object.defineproperty方法提供的getter和setter. 
     *+  3. get函数什么时候执行?
     *+       (1).初次读取时会执行一次。
     *+       (2).当依赖的数据发生改变时会被再次调用。
     *+  4.优势:与methods实现相比， 内部有缓存机制(复用)，效率更高，调试方便。
     *+  5.备注:
     *+       1.计算属性最终会出现在Vm.上， 直接读取使用即可。
     *+       2.如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生
     *+  
     */
    Vue.config.productionTip = false;
    var vm = new Vue({
        el:'#root',
        data:{
            // data保存的是属性
            firstName:'Trump',
            lastName:'Jack'
        },
        computed:{
            // computed保存的是计算属性
            fullName:{
                /**
                 *@  get有什么用?
                 *@  当有人读取fullName时,get就会被调用,且返回值就作为fullName的值
                 *@  get什么时候调用
                 *@  1. 初次读取fullName时
                 *@  2. 所依赖的数据发生变化时
                */
                get(){
                    // 此处的this指向vm
                    return this.firstName + ' ' + this.lastName;
                },
                /**
                 *@ set什么时候调用?
                 *@ 当 fullName被修改时
                */
                set(value){
                    console.log('set',value);
                    // 姓和名通过空格分开
                    const arr = value.split(' ');
                    // 把名和姓也修改了
                    this.firstName = arr[0];
                    this.lastName = arr[1];
                }
            }
        }
    })
</script>
````

#### 监视属性(侦听属性)

* 监视属性 `watch`

  1. 当监视的属性变化时 , 回调函数自动调用 , 进行相关操作

  2. 监视的属性必须存在 , 才能进行监视

  3. 监视的两种写法 :

     * `new Vue` 时传入 `watch` 配置

       ````vue
       watch:{
           isHot:{
               immediate:true,
               handler(newValue,oldValue){
                   console.log('isHot 被修改了',newValue,oldValue);
               }
           }
       }
       ````

     * 通过 `vm.&watch` 监视

       ````vue
       vm.$watch('isHot',{
           immediate:true,
           handler(newValue,oldValue){
               console.log('isHot 被修改了',newValue,oldValue);
           }
       })
       ````

       

  * `handler` 

    > 什么时候调用 ?
    >
    > 当需要监视的属性发生变化时

  * `immediate`

    > immediate 有什么用
    >
    > **初始化时handler调用一下**
    >
    > 默认是false(不调用)

##### 深度监视

1. Vue 中的 watch 默认不检测对象内部值的改变(一层)
2. 配置 `deep:true` 可以检测对象内部值的改变(多层)

**备注 :**

1. Vue 自身可以检测对象内部值的改变 , 但是 Vue 提供的 watch 默认不可以
2. 使用 watch 时根据数据的具体结构 , 决定是否采用深度监测

#### computed和watch之间的区别 :

1. computed 能完成的功能，watch 都可以完成。
2. watch能完成的功能，computed不一 定 能完成，例如: **watch可以进行异步操作**。
3. 两个重要的小原则 : 
   * 所被 Vue 管理的函数，最好写成普通函数，这样 this 的指向才是 vm 或组件实例对象。
   * 所有不被Vue所管理的函数(定时器的回调函数、ajax 的回调函数等)，最好写成箭头函数，这样this的指向才是vm或组件实例对象。

#### 绑定样式:

1. class样式
   * 写法 `:class="xxx"`  
     * xxx可以是字符串、对象、数组。
     * 字符串写法适用于:类名不确定，要动态获取。
     * 对象写法适用于:要绑定多个样式，个数不确定，名字也不确定。
     * 数组写法适用于:要绑定多个样式，个数确定，名字也确定，但不确定用不用。
2. style样式
   * `:style="{fontSize: x}"` 其中xxx是动态值。
   * `:style="[a,b]"` 其中a、b是样式对象。

#### 条件渲染：

1. `v—if`

   写法

   (1)   `.v-if="表达式"`

   (2）`.v—else—if=“表达式”`

​       (3）`.v—else=“表达式”`

​      **适用于：**切换频率较低的场景。

​	  **特点：**不展示的DOM元素直接被移除。

​	  **注意：**` v—if` 可以和：`v—else—if`，` v—else`一起使用，但要求**结构不能被“打断”。**

2. `v—show`

   写法： `v—show=“表达式”`

   适用于：切换频率较高的场景。

   特点：不展示的DOM元素未被移除，仅仅是使用样式隐藏掉

3. 备注：使用`v—if`的时，元素可能无法获取到，而使用`v—show`一定可以获取到。

#### 列表渲染

![image-20210801212006594](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210801212006594.png)

* `v-for` 指令
  * 用于展示列表数据
  * 语法: `v-for="(item,index) in xxx" :key="index"` 
  * 可遍历 : 数组 , 对象 , 字符串(用的很少) , 指定次数(用的很少)

![image-20210801221713172](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210801221713172.png)

![image-20210801221550277](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210801221550277.png)

##### 面试题: react、vue中的key有什么作用? (key的内部原理)

1. 虚拟DOM中key的作用:

   key是虚拟DOM对象的标识，当状态中的数据发生变化时，Vue会根据[新数据]生成[新的虚拟DOM]

   随后Vue进行[新虚拟DOM]与[旧虚拟DOM]的差异比较，比较规则如下:

2. 对比规则: 

   * 旧虚拟DOM中找到了与新虚拟DOM相同的key
     * 若虚拟DOM中内容没变，直接使用之前的真实DOM
     * 若虚拟DOM中内容变了，则生成新的真实DOM，随后替换掉页面中之前的真实DOM
   * 旧虚拟DOM中未找到与新虚拟DOM相同的key
     * 创建新的真实DOM，随后渲染到到页面。

3. 用index作为key可能会引发的问题: 

   * 若对数据进行:逆序添加、逆序删除等破坏顺序操作:
     * 会产生没有必要的真实DOM更新==>界面效果没问题，但效率低。
   * 如果结构中还包含输入类的DOM:
     * 会产生错误DOM更新==>界面有问题。

4. 开发中如何选择key

   * 最好使用每条数据的唯一标 识作为key,比如id、手机号、身份证号、学号等唯一值。
   * 如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，使用index作为key是没有间题的。

![image-20210802125055149](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210802125055149.png)

#### Vue数据监测

Vue监视数据的原理：

1. vue会监视data中所有层次的数据

2. 如何监测对象中的数据？

   通过setter实现监视， 且要在new Vue时就传入要监测的数据

   * 对象中后追加的属性 , Vue 默认不做响应式处理

   * 如需给后添加的属性做响应式，请使用如下API：

     * `Vue.set(target, propertyName/index, value)` 

     * `vm.$set(target, propertyName/index, value)`

3. 如何监测数组中的数据？

   通过包裹数组更新元素的方法实现，本质就是做了两件事：

   * 调用原生对应的方法对数组进行更新。
   * 重新解析模板，进而更新页面。

4. 在Vue修改数组中的某个元素一定要用如下方法：

5. 使用这些API：

   * `push(),pop(), shift(),unshift(), splice(),sort(),reverse()`

   * `Vue.set() 或 vm.$set()`

   **特别注意:** `Vue. set()`和`vm.$set()`**不能给 vm 或 vm的根数据对象 添加属性**

#### 收集表单数据

收集表单数据：

若：`<input type="text"/>` ，则`v-model`收集的是value值，用户输入的就是value值。 

若：`<input type="radio"/>`，则`v-model`收集的是value值，且要给标签配置value值。 

若：`<input type="checkbox"/>`

1．没有配置input的value属性，那么收集的就是checked（勾选 or 未勾选，是布尔值）

2．配置input的value属性：

（1）`v-model`的初始值是非数组，那么收集的就是checked（勾选 or 未勾选，是布尔值）

（2）`v-model`的初始值是数组，那么收集的的就是value组成的数组

备注：`v-model`的三个修饰符：

`lazy`：失去焦点再收集数据

`number`：输入字符串转为有效的数字

`trim`：输入首尾空格过滤

![image-20210802195327209](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210802195327209.png)

#### 过滤器(学的不太明白...) :

* 定义:对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）

* 语法：

  1. 注册过滤器:`Vue．filter（name，callback）`或` new Vue{filters:{}}`

  2. 使用过滤器:`{{xxx|过滤器名}}`或 `v-bind:属性="xxx|过滤器名"`

* 备注:
  1. 过滤器也可以接收额外参数,多个过滤器也可以串联
  2. 并没有改变原本的数据,是产生新的对应的数据

#### 内置指令

`v-bind` ：单向绑定解析表达式，可简写为：xxx

`v-model` ：双向数据绑定

`v-for` ：遍历数组/对象/字符串

`v-on` ：绑定事件监听，可简写为@

`v-if` ：条件渲染（动态控制节点是否存存在）

`v-else` ：条件渲染（动态控制节点是否存存在）

`v-show` ：条件渲染（动态控制节点是否展示）

`v-text` :

* 作用 : 向其所在的节点中渲染文本内容
* 与插值语法的区别 : `v-text` 会替换掉节点中的内容 , `{{xxx}}` 则不会

![image-20210802210613011](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210802210613011.png)

`v-html`

1. 作用：向指定节点中渲染包含html结构的内容。 

2. 与插值语法的区别：

   * `.v-html`会替换掉节点中所有的内容，` {{xx}}`则不会。

   * `.v-html`可以识别html结构。

3. 严重注意： `v-html`有安全性问题！ ！ ！！

   * 在网站上动态渲染任意HTML是非常危险的，容易导致xss攻击。

   * 一定要在可信的内容上使用v—html，永不要用在用户提交的内容上！

`v-cloak`指令（没有值）：

1. 本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉`v-cloak`属性。
2. 使用css配合v—cloak可以解决网速慢时页面展示出`{{xxx}}`的问题。

`v-once`

1. `v-once` 即在节点在**初次动态渲染**后，就视为**静态内容**了。
2. 以后数据的改变不会引起 `v-once` 所在结构的更新，可以用于优化性能。

`v-pre`

1. 跳过其所在节点的编译过程。
2. 可利用它跳过：没有使用指令语法,没有使用插值语法的节点，会加快编译。

#### 自定义指令总结：

##### 一、定义语法： 

1. 局部指令： 

   ````js
   new Vue({
   	directives:{指令名：配置对象}
   })              
   
   或
   new Vue({ 
   	directives: (指令名:函数){}
   })
   
   ````

2. 全局指令：

​      `Vue.directive(指令名，配置对象)`或  `Vue.directive(指令名，回调函数)`

​    *二、配置对象中常用的3个回调：*

​      （1）`.bind`：指令与元素成功绑定时调用。

​      （2）`.inserted`：指令所在元素被插入页面时调用

​      （3）`.update`：指令所在模板结构被重新解析时调用。

​    *三、备注：*

​      1．指令定义时不加 `v-` , 但使用时要加 `v- `;

​      2．指令名如果是多个单词，要使用 `kebab-case`命名方式 ，不要用 camelCase命名

#### 生命周期：

1. 又名：生命周期回调函数、生命周期函数、**生命周期钩子**。

2. 是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数。

3. 生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的。

4. 生命周期函数中的 this 指向是 vm 或组件实例对象。

![生命周期](D:\AFrontEnd\frontEnd\Vue资料\资料（含课件）\02_原理图\生命周期.png)

常用的生命周期钩子：

1. mounted：发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】.
2. beforeDestroy：清除定时器、解绑自定义事件、取消订阅消息等【收尾工作】

关于销毁Vue实例

1. 销毁后借助vue开发者工具看不到任何信息
2. 销毁后自定义事件会失效，但原生DOM事件依然有效。
3. 一般不会再beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程了.

### Vue组件化编程

#### 模块与组件 , 模块化与组件化

* 组件的定义 : 实现应用中**局部**功能**代码**和**资源**的**集合**

##### 模块

1. 理解 : 向外提供特定功能的 JS 程序 , 一般就是一个 JS 文件
2. 为什么 : JS 文件很多很复杂
3. 作用 : 复用 JS , 简化 JS 的编写 , 提高 JS 运行效率

##### 组件

1. 理解 : 用来实现局部 (特定) 功能效果的代码集合(html/css/js/image...)
2. 为什么 : 一个界面的功能很复杂
3. 作用 : 复用编程 , 简化项目编程 , 提高运行效率

##### 模块化

当应用中的 JS 都以模块来编写的 , 那这个应用就是一个模块化的应用

##### 组件化

当应用中的功能都是多组件的方式来编写的 , 那这个应用就是一个组件化的应用



![image-20210803195352849](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210803195352849.png)

#### 非单文件组件

一个文件中包含有 n 个组件

#### 单文件组件

一个文件中只包含一个组件

#### Vue中使用组件的三大步骤：

一、定义组件（创建组件）

二、注册组件

三、使用组件（写组件标签）Ţ

一、如何定义一个组件？

使用`Vue.extend(options)`创建，其中`options`和`new Vue(options)`时传入的那个`options`几乎一样，但也有些区别

区别如下：

1. `el`不要写，为什么？—最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器
2. `data`必须写成函数，为什么？—— 避免组件被复用时，数据存在引用关系。

备注：使用template可以配置组件结构。

二、如何注册组件？

1. 局部注册：靠new Vue的时候传入components选项 
2. 全局注册：靠Vue.component（'组件名',组件） 

三、编写组件标签：

> <school> </school> 

几个注意点：

1. 关于组件名：

​		一个单词组成：

​			第一种写法（首字母小写）： school

​			第二种写法（首字母大写）： School

​		多个单词组成：

​			第一种写法（kebab—case命名）： my—school

​			第二种写法（CamelCase命名）： MySchool （需要Vue脚手架支持）

​		备注：

​			(1)组件名尽可能回避HTML中已有的元素名称，例如： h2，H2都不行。     

​			(2)可以使用name配置项指定组件在开发者工具中呈现的名字。

2. 关于组件标签：

​		第一种写法: ` <school> </school>`

​		第二种写法: `<school/>`

​		备注：不用使用脚手架时,	<school/>会导致后续组件不能渲染

3. 一个简写方式：

   `const school = Vue.extend(options)`

   可简写为: `const school = options`

#### 关于VueComponent：

1. school组件本质是一个名为`VueComponent`的构造函数，且不是程序员定义的，是`Vue.extend`生成的

2. 我们只需要写`<school/>`或`<school> </school>`，Vue解析时会帮我们创建school组件的实例对象， 

​		即Vue帮我们执行的：`new VueComponent(options)`。

3. **特别注意：每次调用`Vue.extend`，返回的都是一个全新的VueComponent！！！！** 

4. 关于this指向：

   * 组件配置中：

     data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是 **[ VueComponent 实例对象 ]**

   * new Vue()配置中：

     data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是 **[ Vue 实例对象 ]**

5. VueComponent的实例对象，以后简称vc（也可称之为：组件实例对象）。

   Vue的实例对象，以后简称vm。

##### 一个重要的内置关系

`VueComponent.prototype.__proto__ === Vue.prototype`

* 为什么有这个关系 : **在组件实例对象 (vc) 可以访问到 Vue 原型上的属性和方法**

![image-20210804102958696](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210804102958696.png)

**实例的隐式原型属性永远指向自己缔造者的原型对象**

组件的定义 : 实现局部代码功能和资源的集合

### Vue 脚手架

#### 脚手架文件结构

* node_modules
* public
  * favicon.ico : 页签图标
  * index.html : 主页面
* src
  * assets : 存放静态资源
    * logo.png 
  * component : 存放组件
    * HelloWorld.vue
  * App.vue : 汇总所有组件
  * main.js : 入口文件
* .gitignore : git 版本管制忽略的配置
* babel.config.js : bable 的配置文件
* package.json : 应用包配置文件
* README.md : 应用描述文件
* package-lock.json : 包版本控制文件

![image-20210804162749248](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210804162749248.png)

#### 关于不同版本的Vue：

1. vue.js 与 vue.runtime.xxx.js 的区别：

​		(1). vue.js 是完整版的 Vue，包含：核心功能＋模板解析器。

​		(2). vue.runtime.xxx.js是运行版的Vue，只包含：核心功能；没有模板解析器。

2. 因为 vue.runtime.xxx.js 没有模板解析器，所以不能使用 template 配置项，需要使用 render 函数接收到的 createElement 函数去指定具体内容。

#### vue.config.js 配置文件

> 使用 vue inspect > output.js 可以查看到 Vue 脚手架的默认配置
>
> 使用 vue.config.js 可以对脚手架进行个性化定制 , 详情见 : https://cli.vuejs.org/zh

#### ref 属性

1. 被用来给玩素或子组件注册引用信息（id的替代者）

2. 用在html标签上获取的是真实DOM元素，应用在组件标签上是组件实例对象（vc）

3. 使用方式：

​	   打标识: `<h1 ref="xxx">......</h1>` 或 `<School ref="xxx"></School>`

​       获取: `this.$refs.xxx`

#### 配置项props

**功能：**让组件接收外部传过来的数据

1. 传递数据：

​			`<Demo name="xxx"/>`

2. 接收数据:

​		第一种方法(只接收)

​		`props:['name']`

​		第二种方式（限制类型）：

> ​	props:{
>
> ​			name:String
>
> ​	}

​		第三种方式(限制类型、限制必要性、指定默认值):

> props:{
>
> ​					name:{
>
> ​						type：String, //类型 
>
> ​						required:true, //必要性
>
> ​						default:'老王' //默认值
>
> ​					}
>
> ​			}

备注：props 是只读的 , Vue 底层会监测你对 props 的修改 , 如果进行了修改,就会发出警告,若业务需求确实需要修改 , 那么请复制 props 的内容到 data 中一份,然后去修改 data 中的数据

#### mixin（混入）

**功能：**可以把多个组件共用的配置提取成一个混入对象

**使用方式：**

第一步定义混合,例如:

````js
{
		data(){···}, 
		methods:{...} 
		....
}
````

第二步使用混入,例如：

​		1.全局混入 : `Vue.mixin(xxx) `

​		2.局部混入 : `mixins:['xxx'] `

#### 插件

* 功能 : 用于增强 Vue

* 本质 : 包含 install 方法的一个对象 , install 的第一个参数是 Vue , 第二个以后的参数是插件使用者传递的数据

* 定义插件

  ````js
  对象.install = function(Vue,options){
  	// 1. 添加全局过滤器
  	Vue.filter(...)
  	// 2. 添加全局指令
  	Vue.directive(...)
  	// 3. 配置全局混入(合)
  	Vue.mixin(...)
  	// 4. 添加实例方法
  	Vue.prototype.$myMethod = function(){...}
  	Vue.prototype.$myProperty = xxx
  }
  
  * 使用插件: Vue.use()
  ````

#### scoped 样式

* 作用 : 让样式在局部生效,防止冲突
* 写法 : `<style scoped>`

![image-20210805105159894](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210805105159894.png)

#### 项目实战

##### 1. 组件化编码流程：

1. 拆分静态组件:组件要按照功能点拆分,命名不要与htm1元素冲突

2. 实现动态组件:考虑好数据的存放位置,数据是一个组件在用,还是一些组件在用:

   * 一个组件在用：放在组件自身即可。

   * 一些组件在用：放在他们共同的父组件上 ( `<span style="color:red">状态提升</span>` ) 

   * 实现交互 : 从绑定事件开始

##### 2. props适用于：

1. 父组件 ==> 子组件通信

2. 子组件 ==> 父组件通信（要求父先给子一个函数）

##### 3.使用 `v-model` 时要切记 : `v-model` 绑定的值不能是 `props` 传过来的值，因为 `props` 是不可以修改的！

##### 4. props传过来的若是对象类型的值，修改对象中的属性时 Vue 不会报错，但不推荐这样做。

#### 浏览器本地存储

WebStorage
1. 存储内容大小一般支持5MB左右(不同的浏览器可能还不一样)
2. 浏览器端通过 Window.sessionStorage 和 Window.localStorage 属性来实现本地存储机制
3. 相关API
    * `xxxxxStorage.setItem('key','value');`
       该方法接收一个键和值作为参数,会把简直对添加到存储中
    * `xxxxxStorage.getItem('person');`
      该方法接收一个键名作为参数,返回键名对应的值
    * `xxxxxStorage.removeItem('key');`
      该方法接收一个键名作为参数,并把该建明从存储中删除
    * `xxxxxStorage.clear()`
      该方法会清空存储中的所有数据
4. 备注:
    1) `SessionStorage` 存储的内容会随着浏览器窗口关闭而消失
    2) `LocalStorage` 存储的内容,需要手懂清除才会消失
    3) `xxxxxStorage.getItem(xxx)`如果xxx对应的value获取不到,那么`getItem`的返回值是null
    4) `JSON.parse(null)`的结果依然是`null`

#### 组件的自定义事件

1. 一种组件间通信的方式,适用于: 子组件 ===> 父组件

2. 使用场景: A是父组件,B是子组件,B想给A传数据,那么就要在A中给B绑定自定义事件(事件的回调在A中)

3. 绑定自定义事件:
    1. 第一种方式,在父组件中,`<Demo @atguigu="test"/>`或`<Demo v-on:atguigu="test"/>`
    
    2. 第二种方式:
    
        ````js
	    <Demo ref="demo"/>
        . . . . . .
        mounted(){
        this.$refs.xxx.$on('atguigu',this.test)
        }
        ````
    
    3. 若想让自定义事件只触发一次,可以使用once修饰符,或$once方法

4. 触发自定义事件:`this.$emit('atguigu',数据)`
5. 解绑自定义事件`this.$off('atguigu')`
6. 组件上也可以绑定原生DOM事件,需要使用native修饰符
7. 注意:通过`this.$refs.xxx.$on('atguigu',回调)`绑定自定义事件.回调要么配置在methods中,要么用箭头函数,否则this的指向会出问题

#### 全局事件总线

全局事件总线(GlobalEventBus)
1. 一种组件间通信的方式,适用于任意组件间通信

2. 安装全局事件总线

  ````js
  new Vue({
   ......
   beforeCreate() {
       Vue.prototype.$bus = this // 按转发全局事件总线,$bus就是当前应用的vm
   },
   ......
  })
  ````

3. 使用事件总线:
    1. 接收数据:A组件想接收数据,则在A组件中给 `$bus` 绑定自定义事件,事件的回调留在A数组自身
    
      ````js
      beforeDestroy(){
       this.$bus.$off('hello')
      }
      methods: {
       demo(data){......}
      },
      ......
      mounted(){
       this.$bus.$on('xxx',this.demo)
      }
      ````
    
    2. 提供数据 : `this.$bus.$emit('xxx',数据)`
    
4. 最好在 `beforeDestroy` 钩子中,用 `$off` 去绑定当前组件所用到的事件

#### 消息订阅与发布（pubsub）

1. 一种组件间通信的方式，适用于任意组件间通信。

2. 使用步骤：

​		1. 安装`pubsub: npm i pubsub-js`

​		2. 引入: `import pubsub from 'pubsub-js'`

  3. 接收数据 :  A组件想接收数据，则在A组件中订阅消息，订阅的回调留在A组件自身。

     ````js
     methods（{
     	demo(data){......}
     }
     mounted() {
      	this.pid = pubsub.subscribe('xxx,this.demo') //订阅消息
     }
     ````

4. 提供数据： `pubsub.publish('xxx',数据)`

5. 最好在`beforeDestroy`钩子中,用`PubSub. unsuyscribe(pid)`去取消订阅。

#### nextTick

1. 语法: `this.$nextTick(回调函数)`
2. 应用: 在下一次DOM更新结束后执行其指定的回调
3. 什么时候应用: 当改变数据后,要基于更新后的新DOM进行某些操作时,要在nextTick所指定的回调函数中执行

Vue 封装的过渡与动画
1. 作用:在插入,更新或移除DOM元素时,在合适的时候给元素添加样式别名

2. 图示

    ![image-20210810145707678](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210810145707678.png)

3. 写法
    * 准备好样式
        + 元素进入时的样式
            - `v-enter` : 进入的起点
            - `v-enter-active` : 进入过程中
            - `v-enter-to` : 进入的终点
        + 元素离开的样式
            - `v-leave` : 离开的起点
            - `v-leave-active` : 离开过程中
            - `v-leave-to` : 离开的终点
        
    * 使用 `<transition>` 包裹要过渡的元素,并配置name属性:
      
        ````html
        <transition name="hello">
            <h1 v-show="isShow">你好啊!</h1> 
        </transition>
        ````
        
    * 备注:若有多个元素需要过渡,则需要使用 `<transition-group>`,且每个元素都要指定`key`值

