title: redux框架-介绍(三大原则)
date: 2015-11-05 13:19:24
tags:
  - react.js
  - redux
categories:
  - redux
---

## Redux 可以被描述成三大基础原则：

### 单一数据源

> 整个应用的 state 被储存在一棵 object tree 中，它只有一个单一的 store 。



这让同构应用开发变得非常容易。来自服务端的 state 可以轻而易举地被序列化并融合到没有额外代码影响的客户端上。
由于是单一的 state tree ，调试也变得非常容易。你也可以把应用的 state 保存下来加快开发速度。
此外，受益于单一的 state tree ，以前难以实现的像“撤销/重做”这类的功能也变得轻而易举。


```
console.log(store.getState());

{
  visibilityFilter: 'SHOW_ALL',
  todos: [{
    text: 'Consider using Redux',
    completed: true,
  }, {
    text: 'Keep all state in a single tree',
    completed: false
  }]

```

### State 是只读的

> 惟一改变 state 的办法就是触发 action，action 是一个描述要发生什么的对象。

这让视图和网络请求不能直接修改 state，相反只能表达出需要修改的意图。
因为所有的修改都被集中化处理，且严格按照顺序一个接一个执行，因此没有模棱两可的情况需要提防。
 Action 就是普通对象而已，因此它们可以被日志打印、序列化、储存、后期调试或测试时回放出来。
 
 ```
 store.dispatch({
  type: 'COMPLETE_TODO',
  index: 1
});

store.dispatch({
  type: 'SET_VISIBILITY_FILTER',
  filter: 'SHOW_COMPLETED'
});
 ```