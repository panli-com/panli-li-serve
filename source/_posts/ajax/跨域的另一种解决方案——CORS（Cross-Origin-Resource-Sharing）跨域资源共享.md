title: 跨域的另一种解决方案——CORS（Cross-Origin Resource Sharing）跨域资源共享
date: 2015-12-02 17:57:45
tags:
  - javascript
  - ajax
categories:
  - javascript
---

在我们日常的项目开发时使用AJAX，传统的Ajax请求只能获取在同一个域名下面的资源，
但是HTML5打破了这个限制，允许Ajax发起跨域的请求。
浏览器是可以发起跨域请求的，比如你可以外链一个外域的图片或者脚本。
但是Javascript脚本是不能获取这些资源的内容的，它只能被浏览器执行或渲染。
主要原因还是出于安全考虑，浏览器会限制脚本中发起的跨站请求。
(同源策略， 即JavaScript或Cookie只能访问同域下的内容)。
跨域的解决方案有多重JSONP、Flash、Iframe等，
当然还有CORS（跨域资源共享，Cross-Origin Resource Sharing）今天就来了解下CORS的原理，以及如何使用。