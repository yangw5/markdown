# REACT

## 基础语法

* ReactDOM.render(...) 进行渲染，ReactDOM.render(<App />, div);

* jsx

  1. html代码嵌入js代码中
  
  1.  HTML 里的 class 在 JSX 里要写成 className，因为 class 在 JS 里是保留关键字。同理某些属性比如 for 要写成 htmlFor。
  
  1.  js代码通过{}包裹

  1.  自定义属性 data-前缀

  1.  props 对象的属性会被设置成 Component 的属性。  {...props} 后面的属性值会覆盖前面的属性。

* Virtual DOM

  组件状态 state 有更改的时候，React 会自动调用组件的 render 方法重新渲染整个组件的 UI。

   Virtual DOM 是一个纯粹的 JS 数据结构
  
*  diff 算法


* 组件 class Welcome extends React.Component  

  小写的字符串是 HTML 标签，大写开头的变量是 React 组件。

  有两个核心概念：

    * state

        是组件的当前状态，一旦状态（数据）更改，组件就会自动调用 render 重新渲染 UI，这个更改的动作会通过 this.setState 方法来触发。

    *  props defaultProps PropTypes

        props是组件的配置属性，在组件内部不可改变，这种组件没有状态，没有生命周期，只是简单的接受 props 渲染生成 DOM 结构。

        props.children表示所有的子元素

  有两种组件

    * 无状态组件

      纯粹的函数来定义无状态的组件，

    * 状态组件

* 生命周期 

  Mounting：已插入真实 DOM

  Updating：正在被重新渲染

  Unmounting：已移出真实 DOM
  
   1. componentWillMount

   1. componentDidMount

   1. componentWillReceiveProps

   1. shouldComponentUpdate

   1. componentWillUpdate

   1. componentDidUpdate  

   1. componentWillUnmount

* 数据自顶向下流动(单项数据流 data flow)

  ction -> Dispatcher -> Store -> View

    ![CSDN图标](flux-overview.png "这是单向数据流原理")


* 事件处理 小驼峰写法  this 

  bind(this) 将事件函数上下文绑定要组件实例上或者通过箭头函数进行绑定,bind(this, arg1, arg2, ...)，第一个参数this,第二个三个...是传递的参数。

* key map

* Refs

  this.refs.name 来访问对应的 DOM 元素。
  
  Refs 是访问到组件内部 DOM 节点唯一可靠的方法

---

## 通信

  * 父子通信

   通过 props 属性传递，在父组件给子组件设置 props，然后子组件就可以通过 props 访问到父组件的数据／方法，这样就搭建起了父子组件间通信的桥梁。

  * 非父子组件间的通信

    使用全局事件 Pub/Sub 模式，在 componentDidMount 里面订阅事件，在 componentWillUnmount 里面取消订阅，当收到事件触发的时候调用 setState 更新 UI。对于比较复杂的应用，推荐使用类似 Flux 这种单项数据流架构

  *  Redux
      
      三个原则：

      1. 整个应用只有唯一一个可信数据源，也就是只有一个 Store
      2. State 只能通过触发 Action 来更改
      3. State 的更改必须写成纯函数，也就是每次更改总是返回一个新的 State，在 Redux 里这种函数称为 Reducer

      * actions

        是一个单纯的包含 { type, payload } 的对象,type 是一个常量用来标示动作类型，payload 是这个动作携带的数据。Action 需要通过 store.dispatch() 方法来发送

      * Reducers

        Reducer 用来处理 Action 触发的对状态树的更改。所以一个 reducer 函数会接受 oldState 和 action 两个参数，返回一个新的 state：(oldState, action) => newState。

      * Store

        store.dispatch
----
  * react-redux 

    * Provider

    * Connect
       
