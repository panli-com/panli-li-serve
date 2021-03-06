title: PanLi app 内嵌厂家页面去除浮动元素 v0.0.2 (注入方案)
date: 2016-01-11 09:59:03
tags:
  - app
  - mobile
  - h5
  - ip
categories:
  - mobile
---

## 应用场景说明

> 在第一版的时候,我们尝试通过 `Panli.com` 主站 ifarme 厂家的各个页面,
> 由于涉及到浏览器安全的问题，浏览器阻住跨域 网站的操作 `dom` 信息 ; 
> 我们只好尝试在 Panli  主站页面 设置遮罩层的方式来弥补
> 随着开发测试的进度一点点完成,最终发现 这个方案不可行

## 注入方案

>在思考许久后， 原生 app 那边 说可以 执行 `javascript`代码 ;

后来我们就开始执行操作， 我们试着写了一下 执行 网页 `dom` 元素的 `javascript` 脚本

最终发现可以操作 web view 厂家页面的 `dom` 元素，可行性方案已找到。

## 开发敏捷

> 在开发注入脚本的时候，在手机上调试结果，非常痛苦,
> 浪费了大量的时间去小心意义的点击 web view 页面 的链接
> 测试机又不给力

无奈之下，既然都是注入 `javascript` 脚本 何不尝试在 `pc` 浏览器上一样注入呢；
我们开发了一套 基于 `Chrome` 浏览器的 插件 。

[插件详细介绍 和 安装](https://github.com/browser-extensions/appRemove)


## 淘宝首页头部元素寻找

![](http://zanjs.b0.upaiyun.com/image/1/f5/52ba910f9917a128b2b0ec64f710f.png)


可以看到在代码区域我看到了 ` id="v539213" class="v61dsk" ` 

我们要录入的元素 就是 id=后面 双引号里面的值 和 class=后面 双引号里面的值

## 数据录入

>为了能及时跟进 各个厂家的 页面的改动 , 
>我们将数据统一后台录入为标准，前台调用接口的形式,来操作厂家 页面元素的去除


### 后台录入如下数据

![](http://zanjs.b0.upaiyun.com/image/4/ae/dd0f6acb0780d2fb129bc0e6e26b3.png)


>id 以#开头，class以.开头
> 录入的数据 以 英文的 `,` 作为分割





### 淘宝客户端广告

在测试数据的时候 , 我们发现 淘宝 头部 的客户端 广告 的 `id`  和 `class` 都是 随机haxi算法生成的。
也就是后台没办法录入这样的数据，因为你录了这次的 `id`  和 `class` 值 页面刷新一下 就又变了,
所以我们只好 在脚本里面写死，根据我们的算法模糊匹配 `id` 和 `class  `

>如果您在寻找 浮动广告元素的 `id` 和 `class` 的时候，
>发现 是 数据和 字母组合的，并且没有意义的组合,请告知我 @julian 。 




 





 




