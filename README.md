# 01 | React出现的历史背景及特性介绍
React 是由Fackbook工程师开发（消息状态错误，上线后检查还是出错，一直调试不好）
#### 为什么会出现 React 这种新框架
```
1,传统UI操作关注太多细节
2.应用程序状态分散在各处,难以追踪和维护
1.传统DOM API关注太多细节
2.React :始终整体"刷新"页面)无需关心细节
```
#### React很简单
```
1.1个新概念
2.4个必须API
3.单向数据流
4.完善的错误提示
```
#### React解决了UI细节问题,数据模型如何解决?
```js
1.传统MVC难以扩展和维护(很难追踪是model出现错误还是view上出错)
2.Flux架构:单向数据流:
WebAPI==>Web API Utils==>Action Creators==>Action==>Dispatcher==>Callbacks==>Store==>Changg Events +Store Queries
==>React Views==>User Interactions==>Action Creators==>Web API Utils==>Web API
相比于传统的MV* 而言，Flux强调单向，从而让整个数据流形成了闭环。
而在MV* 中，数据流往往不会是单向的。
```

#### Flux架构的衍生项目

> Redux 和 Mobx


#### 提到的4个必须的APi具体是指哪四个？
```
1. ReactDOM.render 方法让 React 组件渲染到某个具体的 DOM 节点。
2. 组件的 render 方法 
3. 组件的 setState 方法，用于改变组件状态，触发 render 
4. 如何通过 props 给 React 组件传递参数
```
#### 目前前端react开发主流用什么IDE

> 一般都是 VSCode，不过你也可以尝试 Rekit

#### 老师这里的整体刷新是整个页面刷新嘛，如果这个页面有多个http后端请求，难道所有的http全都要刷新一次嘛？ 这里的store存储的是什么，具体如何通过状态的改变去感知页面的改变，求详解
```js
这里说的整体刷新是指逻辑上纯 UI 的重绘，HTTP 请求一般都在组件的 componentDidMount 或者 componentDidUpdate 中
根据条件来发送，只要逻辑正确，不会每次都重新发起。store 存储的是应用程序状态，包括 UI 状态，例如某个树节点是否展
开，和业务数据状态，比如一个商品列表。页面是根据状态来渲染的，state -> view。 只要通过组件的 this.setState 方法
去改变组件状态，那么页面就会自动更新。
```

#### 怎么理解 Redux ？ 

> 是 React 的进行状态管理的标准

# 02 | 以组件方式考虑UI的构建
 React 组件的概念：将UI组织成组件树的形式

#### 如何理解 React 组件
```
props（外部属性） + state（内部状态） => View（视图）

1.React组件一般不提供方法,而是某种状态机 
2.React组件可以理解为一个纯函数 
3.单向数据绑定
```
####  创建一个简单的组件: TabSelect
```
1.创建静态UI,
2.考虑组件的状态组成 
3.考虑组件的交互方式
```
####  受控组件vs非受控组件
> 受控组件:表单元素状态由使用者维护
```js
<input
 type="text"
 value={this.state.value}
 onChange={evt =>
  this.setState({value:evt.target.value})
 }
/>

```
> 非受控组件:表单元素状态DOM自身维护
```js
<input
 type="text"
 ref={nade => this.input = nade}
/>
```
####  何时创建组件:单一职责原则
```
1.每个组件只做一件事
2.如果组件变得复杂,那么应该拆分成小组件


分成小组件好处：1.提高性能，一个组件大，当发生改变时，整个组件都需要刷新。2.复杂度拆分到不同的地方去
```
####  数据状态管理: DRY原则 
```
1.能计算得到的状态就不要单独存储 （用的时候才计算它，通过其他组件计算得到）
2.组件尽量无状态,所需数据通过 props 获取
```

# 03 | 理解JSX :不是模板语言,只是一种语法糖
```
JSX:在JavaScript代码中直接写HTML标记
JSX的本质:动态创建组件的语法糖
```
####  在JSX中使用表达式
```
1.JSX本身也是表达式    
const element = <h1>Hello, world!</hl>;

2.在属性中使用表达式
<MyComponent foo={1 + 2 + 3 +4} />

3.延展属性
const props = {firstName: 'Ben', lastName: 'Hector'};
const greeting = <Greeting {...props} />;

4.表达式作为子元素
const element = <li>{props.message}</li>;
```
####  JSX优点
```
1.声明式创建界面的直观 
2.代码动态创建界面的灵活 
3.无需学习新的模板语言

```
####  约定:自定义组件以大写字母开头 
```
1. React认为小写的taq是原生DOM节点,如div 
2.大写字母开头为自定义组件
3.JSX标记可以直接使用属性语法,例如<menu.lItem /
```

# 04 | React组件的生命周期及其使用场景
#### React组件的生命周期有三个阶段
```
1."Render阶段"纯净且没有副作用。可能会被React暂停，中止或重新启动.
2."Pre-commit阶段".可以读取DOM。
3."Commit阶段" ,可以使用DOM,运行副作用、安排更新。

```
## React组件的生命周期的组件方法及特性

#### constructor
```
1·用于初始化内部状态,很少使用
2·唯一可以直接修改state的地方
```
#### getDerivedStateFromProps
```
1.当state需要从props初始化时使用
2.尽量不要使用:维护两者状态一致性会增加复杂度 
3.每次render都会调用 
4.典型场景:表单控件获取默认值
```
#### componentDidMount
```
1.UI渲染完成后调用 
2.只执行一次 
3.典型场景:获取外部资源
```
####  componentWillUnmount
````
1.组件移除时被调用 
2.典型场景:资源释放
````
####  getSnapshotBeforeUpdate
```
1,在页面render之前调用, state已更新 
2典型场景:获取render之前的DOM状态
```
####  componentDidUpdate
```
1.每次UI更新时被调用 
2.典型场景:页面需要根据 props变化重新获取数据
```

####  shouldComponentUpdate
```
1.决定Virtual DOM是否要重绘
2.一般可以由PureComponent自动实现 
3.典型场景:性能优化
```

# 05 | 理解 Virtual DOM 及 key 属性的作用
理解Virtual DOM的工作原理,理解key属性的作用

####  JSX的运行基础: Virtual DOM
```
虚拟DOM是如何工作的？局部更新，不需要关注细节
广度优先分层比较
根节点开始比较
属性变化及顺序
节点类型发生变化
节点跨层移动
```
####  虚拟DOM的两个假设
```
1.组件的DOM结构是相对稳定的 
2.类型相同的兄弟节点可以被唯一标识
```

#### 小结
```
1.算法复杂度为O(n)
2.虚拟DOM如何计算diff
3.key属性的作用

```

# 06 | 组件设计模式 : 高阶组件和函数作为子组件

####  组件复用的另外两种形式:高阶组件和函数作为子组件
```
高阶组件(HOC)：对已有组件的分装，形成一个新的组件，包含自己的应用逻辑，新的逻辑产生新的状态，会传给已有的组件
高阶组件一般不会有自己高阶展现，只是负责为分装的组件提供一些额外的功能或者数据。
高阶组件,可以获取外部资源，高阶组件接受组件作为参数,返回新的组件。
```
####  可以实现更多场景的组件复用

# 07 | 理解Context API的使用场景
```
组件通信问题。
React 16.3新特性: Context API

组件树提供
```
# 08 | 使用脚手架工具创建 React 项目

#### 使用脚手架工具创建React应用Create React App, Codesandbox, Rekit

#### 为什么需要脚手架工具
```
React 用来开发
Redux 做React 的状态管理
React Router 做路由的管理
BABEL 用来把最新javascript特性翻译成浏览器能够兼容旧的 javascript 语法，
webpack 用来打包
ESLint 用来做语法检查
```
#### create-react-app
> 这工具 create-react-app，可以快速生成空的React 的项目，快速开始项目的开发。

#### Rekit 整合哪些资源？王沛开发

> create-react-app + Redux + React Router + Less/Scss + Feature Oriented Architecture + Dedicated IDE  = Rekit

#### Online: Codesandbox.io
```
1.主流在线开发平台，
2.不用本地搭建，O配置，直接开发
3.支持 React 、vue 、angular 的开发
```
# 09 | 打包和部署

#### 为什么需要打包?
```
1·编译ES6语法特性,编译JSX ,(1.不能被浏览器直接执行；2.兼用性问题，需要编译转换语法)
2.整合资源,例如图片, Less/Sass 
3.优化代码体积（变量名缩短，去除注释，取数不必要变量名，空格）
```
#### 使用Webpack进行打包
```
所有资源进行整合，
不用关心如何打包，只需关心自己的业务代码应该怎样去写。

```
#### 打包注意事项
```
1.设置nodejs环境为 production
2.禁用开发时专用代码,比如logger 
3.设置应用根路径

```