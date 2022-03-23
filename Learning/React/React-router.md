## React-router



### 什么是react-router

　React-Router 是一个基于React z之上的强大的路由库，它可以让你向应用中快速地添加视图和数据流。同时保持页面与URL之间的同步。



不使用React Router

```react
import React from 'react'
import { render } from 'react-dom'

const About = React.createClass({/*...*/})
const Inbox = React.createClass({/*...*/})
const Home = React.createClass({/*...*/})

const App = React.createClass({
  getInitialState() {
    return {
      route: window.location.hash.substr(1)
    }
  },

  componentDidMount() {
    window.addEventListener('hashchange', () => {
      this.setState({
        route: window.location.hash.substr(1)
      })
    })
  },

  render() {
    let Child
    switch (this.state.route) {
      case '/about': Child = About; break;
      case '/inbox': Child = Inbox; break;
      default:      Child = Home;
    }

    return (
      <div>
        <h1>App</h1>
        <ul>
          <li><a href="#/about">About</a></li>
          <li><a href="#/inbox">Inbox</a></li>
        </ul>
        <Child/>
      </div>
    )
  }
})

React.render(<App />, document.body)
```

当URL的hash 部分（指的是#后的部分）变化后，<App> 会根据this.state.route 来渲染不同的<Child> 看起来和直接，但它很快就会变得复杂起来。



使用React Router 后

```react
import React from 'react'
import { render } from 'react-dom'

// 首先我们需要导入一些组件...
import { Router, Route, Link } from 'react-router'

// 然后我们从应用中删除一堆代码和
// 增加一些 <Link> 元素...
const App = React.createClass({
  render() {
    return (
      <div>
        <h1>App</h1>
        {/* 把 <a> 变成 <Link> */}
        <ul>
          <li><Link to="/about">About</Link></li>
          <li><Link to="/inbox">Inbox</Link></li>
        </ul>

        {/*
          接着用 `this.props.children` 替换 `<Child>`
          router 会帮我们找到这个 children
        */}
        {this.props.children}
      </div>
    )
  }
})

// 最后，我们用一些 <Route> 来渲染 <Router>。
// 这些就是路由提供的我们想要的东西。
React.render((
  <Router>
    <Route path="/" component={App}>
      <Route path="about" component={About} />
      <Route path="inbox" component={Inbox} />
    </Route>
  </Router>
), document.body)
```

React Router 知道如何为我们搭建嵌套的UI， 因此我们不用手动找出需要渲染哪些<Child>组件。举个例子，对于一个完成的`/about`路径，React Router 会搭建出<App><About /></App>

在内部，Router 会将你树级嵌套格式的<Routes转变成路由配置。但如果你不熟悉JSX,你也可以用普通对象来替代。

```react
const routes = {
  path: '/',
  component: App,
  childRoutes: [
    { path: 'about', component: About },
    { path: 'inbox', component: Inbox },
  ]
}

React.render(<Router routes={routes} />, document.body)
```



### Histories

React Router  是建立在history之上的。简而言之，一个history知道如何去监听浏览器地址栏的变化。并解析这个URL转化为location对象。然后router使用它匹配到路由，最后正确地渲染对应的组件。

- <BrowserRouter>
  - http://example.com/about
- <HashRouter>
  - http://example.com/#/about





### react-router解决了什么问题



### 项目中如何使用 react-router



### 有用的API 能帮助你解决什么问题



### 项目中常用的模式。

