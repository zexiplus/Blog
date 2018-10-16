---
title: React 学习总结
---

# react 参考





## Table of content

[TOC]

## react



### 重点

* **关注点分离**: 为每个关注点创建一个组件
* **子节点**: 所有开始标签和结束标签的子节点保存在**this.props.children**属性
* **变量,属性**:使用花括号 {var} 展现变量和属性
* **事件** `<Divider onClick={this.handleClick} />`
* **ref.myinput.getDOMNode()** 拿到真实dom节点
* class属性要写为**className**

#### 生命周期&钩子

* **生命周期: 实例化, 存在期, 销毁&清理期**

  * 实例化
    * getDefaultProps
    * getInitialState (**此时可以访问this.props**)
    * componentWillMount
    * render
    * componentDidMount

  * 存在期
    * componentWillReceiveProps
    * shouldComponentUpdate (首次渲染不会调用) 
    * componentWillUpdate
    * componentDidUpdate

  * 销毁清理期
    * componentWillUnmount

#### 数据&属性

* 在react中,数据(props)是**单向流动**的， 从父节点传递到子节点， 禁止一个组件修改自己的props
* **props**,用于管理从外部传入的数据。 `<MyComponent list={list} />`  钩子**getDefaultProps (() => {showOpt: true})  **
* **state** , 用于管理组件自身的数据。 钩子 **getInitialState(() => {showOpt: true})**   
* 修改(合并)state：   **this.setState({value: 1})**  , 替换 **state this.replaceState({value: 1})**
* 只要setState调用， render就会被调用,  不要直接赋值给 state
* 把props当作**只读**， **state尽量存放简单数据** 例如表单控件的隐藏和显示
* **属性检查**  ` { propTypes: {id: React.PropType.string.isRequired}}`

#### 事件

* **手动开启触控事件** React.initialzeTouchEvents(true)

* **绑定事件** `<Component onClick="this.handleClick" />`

* 事件的值 **event.target.value**

* 父子组件通讯  父组件通过单向props传递给子组件， 子组件通过传递的事件进行通信

  ```jsx
  class Sup extends React.Component {
      constructor(props) {
          super(props)
          this.handleChange = this.handleChange.bind(this)
      }
      handleChange(e) {}
      render() {
          return (<Sub onChange={this.handleChange} />)
      }
  }
  class Sub extends React.Component {
      constructor(props) {
          supper(props)
      }
      render() {
          return (<select onChange={this.props.onChange}></select>)
      }
  }
  ```

#### 组件

* 受控组件 ， 组件内部状态由用户管理， 最简单的实现就是一个 自定义表单输入框
* 非受控组件 ， 组件内部状态不可控 ,用在不做任何校验的场景

* ref.id.**getDOMNode**() 获取真正的dom节点， 此方法在componentDidMount可访问

* **整合非react类库** , 在**componentDidMount**函数中访问dom节点， 写逻辑

  ```jsx
  class AnimateBox extends React.Component {
      constructor(props) {
          super(props)
      }
      render() {
          return (
          	<div ref="box" id="animateBox" >0</div>
          )
      }
      componentDidMount() {
          animate({el: this.ref.box.getDOMNode(), type: 'rotate'})
      }
  }
  ```

#### 性能优化

* 使用**shouldComponentUpdate** 来判断组件是否需要重新渲染， 返回 true 代表需要重新渲染

  ```jsx
  {
      shouldComponentUpdate(nextProps, nextState) {
          return nextProps.id !== this.props.id // 只有id更新才更新组件
      }
  }
  ```

* 使用**React.addons.PureRenderMixin**插件

  ```jsx
  {
      mixin: [React.addons.PureRenderMixin]
  }
  ```

* 监控性能变化插件 **React.addons.Perf**

  ```shell
  // 控制台运行
  React.addons.Perf.start()
  // 操作应用， 记录耗时的操作
  React.addons.Perf.stop()
  // 打印时间表单
  React.addons.Perf.printWaster()
  ```

* 为列表添加**key属性**， 避免重复渲染。









### react 组件结构

```jsx
class MarkdownEditor extends React.Component {
    constructor(props) {
        super(props)
        this.handleChange = this.handleChange.bind(this)
        this.state = { value: 'Type your markdown'}
    }
    
    handleChange(e) {
        this.setState({ value: e.target.value })
    }
    
    generateMarkdown() {
        const md = new Remarkable();
        return { __html: md.render(this.state.value) }
    }
    
    render() {
        return (
        	<div>
            	<textarea 
                    onChange={this.handleChange} 
                    defaultValue={this.state.value} />
                <h1>output markdown</h1>
                <div 
                    className="output"
                    dangerouslySetInnerHTML={this.generateMarkdown()}
                 />
            </div>
        )
    }
}
```





### 脚手架

* **Create-react-app(官方)**

  > https://github.com/facebook/create-react-app

  * 使用

    ```bash
    # using npm
    npm init react-app my-app
    
    # using yarn
    yarn create react-app my-app
    ```



### Assets

* **Import img**

  ```jsx
  import logo from './logo.png'
  function Photo() {
      return <img src={logo} alt="logo" />
  }
  ```

* **import css**

  ```jsx
  import './css/app.css'
  ```


### API

- **ReactDOM.render**

  > 在指定dom元素上渲染react元素

  ```jsx
  const element  = <img src={img.url} />
  const dom = document.querySelector('.pic')
  ReactDOM.render(element, dom)
  ```




### JSX

* **普通表达式**

  ```jsx
  const element = <div>hello world</div>
  ```

* **嵌入表达式**

  > 使用单层括号使用变量, 函数 { variable } 

  ```jsx
  const name = 'float'
  const userinfo = (person) => {
      return `person's name is ${person.name} age is ${person.age}`
  }
  
  const element = <div>hello, {name}</div>
  const element2 = <div>hello, {userinfo({name: 'float'})}</div>
  ReactDOM.render(element, document.querySelector('body'))
  ```



### Components and props

* **Functional components**

  > 函数组件

  ```jsx
  function Welcome (props) {
      return <div>hello  {props.name}</div>
  }
  
  const welcome = <Welcome name="float"></Welcome>
        
  ReactDOM.render(welcome, document.querySelector('body'))
  ```

* **class components**

  > 类组件

  ```jsx
  class Tittle extends React.Component {
      render() {
          return <h1>this is a tittle {this.props.name}</h1>;
      }
  }
  
  // 渲染类组件
  const tittle = <Tittle name="float" />
  ```

* **composing components**

  > 嵌套组件

  ```jsx
  function Parent(props) {
      return 
          <div id={props.id}>
      		<Sub index="1"></Sub>
          	<Sub index="2"></Sub>
      	</div>;
  }
  
  function Sub(props) {
      return <p>{props.index}</p>
  }
  ```

* **Read-only props**

  > 组件的属性是只读的

  ```jsx
  // do not use like this
  function Title(props) {
      props.name += 'tail'
      return <h1>name is {}</h1>
  }
  ```



### Life circle

> 组件生命周期钩子函数

* 





### State

* **init state**

  > 使用constructor 初始化state

  ```jsx
  class Num extends React.Component {
      constructor(props) {
          super(props)
          // state只可以在constructor中可以直接赋值
          this.state = {num: 1}
      }
      
      render() {
          return <div>num is {this.state.num}</div>
      }
  }
  ```

* **hooks**

  > 钩子函数改变state

  ```jsx
  class Clock extends React.Component {
      refreshClock() {
          this.setState({time: new Date()})
      }
      componentDidMount() {
          this.clockId = setInterval(() => this.refreshClock(), 1000)
      }
      componentWillUnmount() {
          this.clearInterval(this.clockId)
      }
  }
  ```

* **setState**

  > 改变state

  ```jsx
  // 对象作为参数
  this.setState({
      name: 'float',
      age: 24
  })
  
  // 函数作为参数, 用于引用state, props
  this.setState((state, props) => ({
      num: props.num + 1
  })
  ```

* **share state**

  > 当两个组件需要共享state时, 提升state

  ```jsx
  class ParentState extends React.Component {
    constructor(props) {
      super(props)
      this.saveNum = this.saveNum.bind(this)
      this.state = {
        num: 0
      }
    }
    saveNum(e) {
      this.setState({
        num: e.target.value
      })
    }
    render() {
      return (
        <div>
          <SubState num={this.state.num} tag='small' onHandleChange={this.saveNum} />
          <SubState num={this.state.num} tag='big' onHandleChange={this.saveNum} />
        </div>
      );
    }
  }
  
  class SubState extends React.Component {
    constructor(props) {
      super(props)
    }
    render() {
      let num = this.props.num
      if (this.props.tag === 'big') {
        num = Number(num) + 5
      }
      let changeHandler = this.props.onHandleChange
      return (
        <div>
          <input value={num} onChange={changeHandler} />
        </div>
      );
    }
  }
  ```


### Event

* **event binding**

  > 事件绑定

  ```jsx
  <button onClick={postData}></button>
  ```

* **preventDefault**

  > 阻止事件默认行为

  ```jsx
  function Submit(props) {
      function postData(e) {
          e.preventDefault()
          // do some thing
      }
      return (
      	<div>
          	<a href="#" onClick={postData}></a>
          </div>
      )
  }
  ```

* **params**

  > 事件传参

  ```jsx
  <button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
  <button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
  ```



### Conditional render

* **state conditional using if**

  ```jsx
  class LoginControl extends React.Component {
      constructor(props) {
          super(props)
          this.state = {
              isLogin: false
          }
      }
      
      login() {
          this.setState({ isLogin: true , username: 'float'})
      }
      logout() {
          this.setState({ isLogin: false })
      }
      
      render() {
  		const isLoginFlag = this.state.isLogin
          let template
          if (isLoginFlag) {
              template = (
              	<div>
                  	<p>welcome {this.state.username}</p>
                      <button onClick={this.logout}></button>
                  </div>
              );
          } else {
              template = (
              	<div>
                  	<p>please login</p>
                      <button onClick={this.logout}></button>
                  </div>
              );
          }
          
          return (
          	<div>
              	<p>this is login component</p>
                  {template}
              </div>
          )
      }
  }
  ```



### List

* **render list**

  > 列表的渲染, 必须有全局唯一 key 属性

  ```jsx
  function List(props) {
      return (
      	<ul>
              {
                  props.numbers.map( item => <li key={item.value.toString()}>{item.value}</li>)
              }
          </ul>
      )
  }
  ```




### Form

* 表单的渲染与事件绑定

  ```jsx
  class Form extends React.Component {
    constructor(props) {
      super(props)
      this.state = { name: '' }
      this.handleValueChange = this.handleValueChange.bind(this)
    }
    handleValueChange(e) {
      this.setState({name: e.target.value})
    }
    render() {
      return (
        <form>
          <label>type your name</label>
          <input value={this.state.name} onChange={this.handleValueChange} />
          <span>{this.state.name}</span>
        </form>
      );
    }
  }
  ```



### Children

* **props.children**

  > 非命名子属性, 使用props.children 属性组合其他组件的内容

  ```jsx
  class Mavic extends React.Component {
      constructor(props) {
          super(props)
      }
      fly() {
  		console.log('I can fly')
      }
      render() {
  		return (
  			<div className={'colorful' + this.props.color}>
              	{this.props.children}
              </div>
          );
      }
      
  }
  
  class MavicPro extends React.Component {
      constructor(props) {
          super(props)
      }
      fly() {
          console.log(' I can fly 60km/h')
      }
      render() {
          <div>
          	<Mavic>
                  <span>hi I am mavic pro</span>
                  <button>click to buy me</button>
              </Mavic>
              
          </div>
      }
  }
  ```

* **props.left ...**

  > 命名子属性

  ```jsx
  function TableContent(props) {
    return (
      <div>
        <div className="left">
          {props.left}
        </div>
        <div className="right">
          {props.right}
        </div>
      </div>
    );
  }
  
  function RandL() {
    let left = <div>hello left</div>
    let right = <div>hello right</div>
    return (
      <div>
        <TableContent
          left={left}
          right={right}
        />
      </div>
    );
  }
  ```



## react router

路由

### 初始化

* **install**

  ```shell
  npm install react-router-dom
  ```

* **using router** 

  ```jsx
  // app.js
  import { Route, Link, BrowserRouter as Router } from 'react-router-dom'
  
  const routing = (
  	<Router>
      	<div>
          	<Route exact path="/" component={App} />
              <Route path="/users" component={User} />
              <Route path="/contract" component={Contract} />
          </div>
      </Router>
  )
  
  ReactDOM.render(routing, document.querySelector('#root'))
  ```

  * exact 属性: 精确匹配, 若不加此属性, /users 和 /contract会匹配到 /



### Tag

* **link**

  ```jsx
  const routing = (
  	<Router>
      	<div>
          	<ul>
              	<li><Link to="/">home</Link></li>
                  <li><Link to="/users">users</Link></li>
                  <li><Link to="/contract">contract</Link></li>
              </ul>
              <Route path="/" component={App} />
              <Route path="/users" component={Users} />
              <Route path="/contract" component={Contract} />
          </div>
      </Router>
  )
  ```

* **Switch**

  > Switch 标签用于匹配notfound page

  ```jsx
  <Router>
  	<Link to="/">home</Link>
      <Switch>
      	<Route path="/" component={Home} />
          <Route component={NotFound} />
      </Switch>
  </Router>
  ```

* **BrowserRouter && HashRouter**

  > 两种路由, 浏览器路由和静态哈希路由(浏览器地址栏带有#)

  ```jsx
  import { BrowserRouter, HashRouter } from 'react-router-dom'
  function Router() {
      return (
      	<BrowserRouter>
          	<link></link>
              <Router />
          </BrowserRouter>
      )
  }
  ```






