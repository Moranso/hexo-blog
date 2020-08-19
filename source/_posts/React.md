---
title: React
date: 2019-04-01 20:05:46
tags:
---

### React

**React 是一个采用声明式，高效且灵活的用来构建用户界面的框架,会根据应用数据的变化自动渲染和更新组件**。

#### 脚手架搭建项目目录

```
新建项目目录
cd 项目目录
yarn create umi
安装依赖	yarn
yarn start 启动服务
```

#### npm run eject 弹出webpack配置,报错解决办法

```
git add .
git commit -am "Save before ejecting"
再使用 npm run eject
```

#### JSX

它是JavaScript的语法扩展,它由js表达式和html标签组成,在编译之后会转化成普通的JavaScript对象

JS表达式用 {} 包裹,JSX允许在大括号中嵌入任何表达式

#### React DOM

React元素创建之后不可变,但可以用其他方法去更新DOM,React Dom会比较元素先后的内容,只更新改变的部分

#### 组件&Props

组件可以将UI切分成一些独立的、可复用的部件，它可以接收任意的输入值（props），并返回一个需要在页面上展示的React元素

输入的数据通过 `this.props` 传入 `render()` 方法

无论是使用[函数或是类](https://react.docschina.org/docs/components-and-props.html#%E5%87%BD%E6%95%B0%E5%AE%9A%E4%B9%89/%E7%B1%BB%E5%AE%9A%E4%B9%89%E7%BB%84%E4%BB%B6)来声明一个组件，它决不能修改它自己的props

### ES6定义组件(类组件,有一些额外特性) 

#### 额外特性

- 私有状态(state)
- 生命周期钩子

```
import React, { Component } from "react";
import React from 'react';
import ReactDOM from 'react-dom';
import './Header.css'

class Header extends Component {
  render() {
    const time = new Date().toLocaleTimeString()
    return (
      <div className="Header">
        Hello {time}
      </div>
    )
  }
}
```

### 渲染组件

```
ReactDOM.render(<Header />, document.getElementById('root'))
```

### State&生命周期

状态与属性十分相似,但是状态是当前组件私有的

#### 为一个类组件添加局部状态(state)

```
import React, { Component } from "react";
import './Header.css'

class Header extends Component {
  constructor(props) {
    super(props)
    //初始化局部状态
    this.state = {date: new Date()}
  }
  tick() {
    this.setState({
      date: new Date()
    })
  }
  // 组件渲染之后生成dom
  componentDidMount() {
    this.timer = setInterval(() => {
      this.tick()
    }, 1000);
  }
  // 卸载组件
  componentWillUnmount() {
    clearInterval(this.timer)
  }
  render() {
    return (
      <div className="Header">
        Hello {this.state.date.toLocaleTimeString()}
      </div>
    )
  }
}

export default Header
```

this.state  =  {}	//初始化局部状态

this.setState({})	//更改局部状态

#### 注意

- 不能直接更改状态  更改状态需要用 setState()

- this.props 和 this.state 可能是异步更新的,不能依靠它们的值来计算下一个状态

  如果需要修复它, setState() 接收一个函数作为参数

  ```
  this.setState((prevState, props) => ({
    counter: prevState.counter + props.increment
  }));
  
  第一个参数(prevStaste): 先前的状态(对象)
  第二个参数(props): 此次更新被应用时的props
  ```

- 组件可以将其状态作为属性传递给其子组件(**子组件不知道是来自父组件的状态(state)还是属性(props)**)  ---  **单向数据流**

#### 生命周期

###### 初始化

- getDefaultProps()	-->	设置默认的props,也可以用defaultProps设置组件的默认属性
- getInitialState()            -->         类组件没有这个钩子函数,*可以直接在constructor中定义this.state。此时可以访问this.props*
- componentWillMount()     -->     *组件初始化时只调用，以后组件更新不调用，整个生命周期只调用一次，此时可以修改state。*
- render()           -->              *react最重要的步骤，创建虚拟dom，进行diff算法，更新dom树都在此进行。此时就不能更改state了。*
- componentDidMount()        -->          *组件渲染之后调用，只调用一次。*

###### 更新

- *componentWillReceiveProps(nextProps)*       -->          *组件接受新的props时调用。*
- *shouldComponentUpdate(nextProps, nextState)*        -->        *react性能优化非常重要的一环。组件接受新的state或者props时调用，我们可以设置在此对比前后两个props和state是否相同，如果相同则返回false阻止更新，因为相同的属性状态一定会生成相同的dom树，这样就不需要创造新的dom树和旧的dom树进行diff算法对比，节省大量性能，尤其是在dom结构复杂的时候*
- *componentWillUpdata(nextProps, nextState)*       -->        *组件将要更新时才调用，此时可以修改state*
- *render()*     -->       组件渲染
- *componentDidUpdate()*     -->       *组件更新完成后调用，此时可以获取dom节点。*

###### 卸载

- *componentWillUnmount()*        -->      *组件将要卸载时调用，一些事件监听和定时器需要在此时清除。*

### 事件处理

React 元素的事件处理和 DOM元素的很相似,但有一些语法区别

- React事件绑定属性的命名采用驼峰式写法，而不是小写
- 如果采用 JSX 的语法你需要传入一个函数作为事件处理函数，而不是一个字符串(DOM元素的写法)

```
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

#### 注意

- 在React中不能使用return false 阻止默认行为,必须明确使用 e.preventDefault

- 类的方法默认是不会[绑定](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_objects/Function/bind) `this` 的 

  **解决办法是 类方法 使用箭头函数**

  ```
  import React, { Component } from 'react';
  import logo from './logo.svg';
  import './App.css';
  import Header from './Header/Header'
  
  class App extends Component {
    constructor(props) {
      super(props)
      this.state = {
        flag: true
      }
    }
    handleClick = () => {
      this.setState(prevState => ({
        flag: !prevState.flag
      }))
    }
    btnClick = (name, e) => {
      alert(name)
      console.log(e)
    }
    render() {
      return (
        <div>
          <Header />
          <div onClick={ this.handleClick }>
            {this.state.flag ? 'on' : 'off'}
          </div>
          <div className="" onClick={(e) => this.btnClick('name', e)}>
            按钮
          </div>
        </div>
      )
    }
  }
  
  export default App;
  
  ```

  #### 父子组件传参

  **父传子**   --->   父组件绑定一个属性 子组件 super(props)

  ```
  <Post key={post.id} id={post.id} title={post.title} />
  
  ```

  #### 条件渲染

  ...

  #### 列表渲染&keys

  Keys可以在DOM中的某些元素被增加或删除的时候帮助React识别哪些元素发生了变化

  ```
  import React, { Component } from 'react';
  import logo from './logo.svg';
  import './App.css';
  import Header from './Header/Header'
  
  class App extends Component {
    constructor(props) {
      super(props)
      this.state = {
        
      }
    }
    render() {
    	const numbers = [1, 2, 3, 4, 5]
      const listItems = numbers.map(item => <li key={item}>{item}</li>)
      return (
        <div>
          <ul>
            {listItems}
          </ul>
        </div>
      )
    }
  }
  
  export default App;
  
  ```

  #### 表单

  React的表单元素生来就保留一些内部状态

  ##### 受控组件

  **value属性可读写  官方推荐 value值由组件状态(state)控制**

  像`<input>`,`<textarea>`, 和 `<select>`这类表单元素,可变的状态通常保存在组件的状态属性中

  处理提交表单并可访问用户输入表单数据的函数叫作"**受控组件**"的技术 (setState()方法进行更新)

  ```
  import React, {Component} from 'react'
  import './Form.css'
  
  class Form extends Component {
    constructor(props) {
      super(props)
      this.state = {
        value: ''
      }
    }
    handleChange = (e) => {
      this.setState({
        value: e.target.value
      })
    }
  
    render() {
      return (
        <div className="main">
          {/* Form */}
          <form>
            <span>姓名: </span>
            <input type="text" value={this.state.value} onChange={this.handleChange} />
          </form>
          <div>
            {this.state.value}
          </div>
        </div>
      )
    }
  }
  
  export default Form
  
  ```

  在HTML当中，`<textarea>` 元素通过子节点来定义它的文本内容,在React中，`<textarea>`会用`value`属性来代替

  ##### 非受控组件

  在大多数情况下，我们推荐使用 [受控组件](https://react.docschina.org/docs/forms.html) 来实现表单。 在受控组件中，表单数据由 React 组件处理。如果让表单数据由 DOM 处理时，替代方案为使用非受控组件。

  ```
  class NameForm extends React.Component {
    constructor(props) {
      super(props);
      this.handleSubmit = this.handleSubmit.bind(this);
    }
  
    handleSubmit(event) {
      alert('A name was submitted: ' + this.input.value);
      event.preventDefault();
    }
  
    render() {
      return (
        <form onSubmit={this.handleSubmit}>
          <label>
            Name:
            <input type="text" ref={(input) => this.input = input} />
          </label>
          <input type="submit" value="Submit" />
        </form>
      );
    }
  }
  
  ```

  #### 状态提升(组件传参 子传父 父再把状态分发给其他子组件)

  React中的状态提升概括来说,就是将多个组件需要共享的状态提升到它们最近的父组件上.在父组件上改变这个状态然后通过props分发给子组件.

  **子组件通过在props属性上绑定一个自定义事件名** **参数为提升的数据** 

  **父组件绑定这个事件名得到子组件传递出来的数据**

  ```
  import React, {Component} from 'react'
  import './Foo.css'
  
  class Child_1 extends Component {
    constructor(props) {
      super(props)
    }
    render() {
      return (
        <div>
          <h1>{this.props.name + '我是第一个子组件'}</h1>
        </div>
      )
    }
  }
  
  class Child_2 extends Component {
    constructor(props) {
      super(props)
    }
    render() {
      return (
        <div>
          <h1>{this.props.name + '我是第二个子组件'}</h1>
        </div>
      )
    }
  }
  
  //状态提升的关键步骤
  class Input extends Component {
    constructor(props) {
      super(props)
    }
    handleChange = (e) => {
      // this.props.name = e.target.value
      this.props.changeName(e.target.value)
    }
    render() {
      return (
        <div>
          <input type="text" value={this.props.name} onChange={this.handleChange} />
        </div>
      )
    }
  }
  
  class Foo extends Component {
    constructor(props) {
      super(props)
      this.state = {
        txt: ''
      }
    }
    handleChange = (txt) => {
      this.setState({
        txt: txt
      })
    }
    render() {
      return (
        <div className="Foo">
          <Input name={this.state.txt} changeName={this.handleChange} />
          <p>{this.state.txt}</p>
          <Child_1 name={this.state.txt} />
          <Child_2 name={this.state.txt} />
        </div>
      )
    }
  }
  
  export default Foo
  
  ```

  #### 组合 VS 继承

  React 具有强大的组合模型，我们建议使用组合而不是继承来复用组件之间的代码。

  组件可以接受任意元素，包括基本数据类型、React 元素或函数。

  ##### 包含关系

  推荐 组件作为属性传递给子组件

  ```
  import React, {Component} from 'react'
  import './Foo.css'
  
  class Foo extends Component {
    constructor(props) {
      super(props)
    }
  
    render() {
      return (
        <div className="foo">
          <div className="left">
            {this.props.left}
          </div>
          <div className="right">
            {this.props.right}
          </div>
        </div>
      )
    }
  }
  export default Foo
  
  
  import React, { Component } from 'react';
  import logo from './logo.svg';
  import './App.css';
  import Header from './Header/Header'
  import Form from './Form/Form'
  import Foo from './Foo/Foo'
  import Foo_1 from './FooBar/Foo'
  
  class Left extends Component {
    constructor(props) {
      super(props)
    }
    render() {
      return <div>我是左边的子组件</div>
    }
  }
  
  class Right extends Component {
    constructor(props) {
      super(props)
    }
    render() {
      return <div>我是右边的子组件</div>
    }
  }
  
  class App extends Component {
    constructor(props) {
      super(props)
    }
  
    render() {
      return (
        <div>
          <Foo_1 
            left={
              <Left />
            }
            right={
              <Right />
            }
          />
        </div>
      )
    }
  }
  export default App;
  
  
  ```

  [redux参考文章]: https://www.cnblogs.com/luozhihao/p/5660496.html	"redux参考文章"
  [dva]: https://dvajs.com/guide/getting-started.html#%E5%AE%89%E8%A3%85-dva-cli
  [umi]: https://umijs.org/zh/guide/create-umi-app.html

  