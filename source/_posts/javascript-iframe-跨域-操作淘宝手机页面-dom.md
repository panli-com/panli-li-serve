title: javascript iframe 跨域 操作淘宝手机页面 dom
date: 2015-12-09 16:57:28
tags:
  - javascript
  - webapp
  - 跨域
categories:
  - javascript	
---


## javascript 操作 iframe

正常情况下 `javascript` 可以正常操作 `iframe` 的子页面元素

![js操作 iframe 的子页面元素](http://zanjs.b0.upaiyun.com/image/2/ba/307edada2e2ca9cc420ffa81268bb.gif)


而在尝试 `iframe` 引入 淘宝页面的时候 却操作不了 



![js操作 跨域 iframe 的子页面元素](http://zanjs.b0.upaiyun.com/image/7/4f/c416ff8f03dd5afb65488037720f8.gif)

浏览器报错信息如下

```
Uncaught DOMException: Failed to read the 'contentDocument' property from 'HTMLIFrameElement':
 Blocked a frame with origin "http://localhost:3000" from accessing a cross-origin frame.(…)
```


可以看出来 浏览器阻止了 跨域操作的请求，操作后 感觉肯定有解决的方案

##  寻找解决方案

先百度后谷歌

百度情况很槽糕，没有我想要的答案， 于是就是去了 `segmentfault ` 

找到了 类似的 需求  http://segmentfault.com/q/1010000002670960


找到的答案就是  

1. `浏览器会限制跨与操作的，除非你是为浏览器开发插件，可以绕过权限`
2. `无解，只能通过后端。`



然后 谷歌 寻找更加专业的 解决方案

我来到了 `stackoverflow` 寻找解决方案  

地址是  http://stackoverflow.com/questions/6170925/get-dom-content-of-cross-domain-iframe


被认知的 答案 是 


>You can't. XSS protection. Cross site contents can not be read by javascript.
>No major browser will allow you that. 
>I'm sorry, but this is a design flaw, you should drop the idea.


大概意思就是 ：不可能，浏览器 xss 保护 ，跨域网站的内容不能被JavaScript 操作，目前只好放弃这种想法，不知未来是否有改善。


## 问题总结

目前而言 对应前端来说真是没有解决方案了，好无奈， 而我能想到的就是  后端做服务了 ， 抓到页面内容渲染到前端显示操作，就不存在 跨域的问题了

如果您找到了更好的解决方案， 欢迎留言交流 ！！



