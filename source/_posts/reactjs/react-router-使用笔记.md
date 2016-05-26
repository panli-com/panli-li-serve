title: react-router 使用笔记
date: 2016-05-26 17:08:07
tags:
    - reactjs
    - react-router
categories:
    - reactjs
---

真正学会 [React](https://facebook.github.io/react/) 是一个漫长的过程。

![漫长的过程](../../update/20160526/lu.jpg)


你会发现，它不是一个库，也不是一个框架，而是一个庞大的体系。
想要发挥它的威力，整个技术栈都要配合它改造。
你要学习一整套解决方案，从后端到前端，都是全新的做法。


![reactjs](../../update/20160526/react.png)

举例来说，React 不使用 HTML，而使用 JSX 。
它打算抛弃 DOM，要求开发者不要使用任何 DOM 方法。
它甚至还抛弃了 SQL ，自己发明了一套查询语言 GraphQL 。
当然，这些你都可以不用，React 照样运行，但是就发挥不出它的最大威力。


这样说吧，你只要用了 React，就会发现合理的选择就是，采用它的整个技术栈。


本文介绍 React 体系的一个重要部分：路由库 [React-Router](https://github.com/reactjs/react-router)。
它是官方维护的，事实上也是唯一可选的路由库。
它通过管理 URL，实现组件的切换和状态的变化，开发复杂的应用几乎肯定会用到。



另外，我没有准备示例库，因为官方的[示例库](https://github.com/reactjs/react-router-tutorial/tree/master/lessons)非常棒，由浅入深，分成14步，每一步都有详细的代码解释。
我强烈建议你先跟着做一遍，然后再看下面的API讲解。


## 基本用法

React Router 安装命令如下。

```
npm install -S react-router
```

使用时，路由器 `Router` 就是 `React` 的一个组件

```
import { Router } from 'react-router';

//...

render(<Router/>, document.getElementById('app'));
```


`Router` 组件本身只是一个容器，真正的路由要通过 `Route` 组件定义


```
import { Router, Route, hashHistory } from 'react-router';

render((
  <Router history={hashHistory}>
    <Route path="/" component={App}/>
  </Router>
), document.getElementById('app'));
```


上面代码中，用户访问根路由 `/` 比如 `http://www.example.com/）`，

组件 `APP ` 就会加载到 `document.getElementById('app')` 。

你可能还注意到，`Router ` 组件有一个参数 `history`，

它的值 `hashHistory` 表示，

路由的切换由 `URL` 的 `hash` 变化决定，即 `URL` 的 `#` 部分发生变化。

举例来说，用户访问 `http://www.example.com/`，

实际会看到的是 `http://www.example.com/#/`。

`Route` 组件定义了URL路径与组件的对应关系。你可以同时使用多个 `Route `组件。


[更多原文](http://www.ruanyifeng.com/blog/2016/05/react_router.html)



