title: 使用Flexible实现手淘H5页面的终端适配 笔记之(1) 简介篇
date: 2016-01-08 09:50:36
tags:
 - webapp
 - mobile
 - h5
 - Flexible
 - 终端适配
categories:
  - mobile
---

## 出入江湖

> 曾几何时为了兼容IE低版本浏览器而头痛，以为到Mobile时代可以跟这些麻烦说拜拜。
> 可没想到到了移动时代，为了处理各终端的适配而乱了手脚。
> 对于混迹各社区的偶，时常发现大家拿手机淘宝的H5页面做讨论——手淘的H5页面是如何实现多终端的适配？


那么趁此Amfe阿里无线前端团队双11技术连载之际，用一个实战案例来告诉大家，
手淘的H5页面是如何实现多终端适配的，希望这篇文章对大家在Mobile的世界中能过得更轻松。

## 目标


拿一个双11的Mobile页面来做案例，比如你实现一个类似下图的一个H5页面：

![](https://camo.githubusercontent.com/5ac077a46fc12456b71725f70cab904abcffb6e7/687474703a2f2f7777772e773363706c75732e636f6d2f73697465732f64656661756c742f66696c65732f626c6f67732f323031352f313531312f72656d2d312e6a7067)


目标很清晰，就是做一个这样的H5页面。

## [demo](http://huodong.m.taobao.com/act/yibo.html)

请用手机扫下面的二维码

![](https://camo.githubusercontent.com/ed811c9fc57a03fe46ef716921a221a678bb1160/687474703a2f2f7777772e773363706c75732e636f6d2f73697465732f64656661756c742f66696c65732f626c6f67732f323031352f313531312f7969626f71722e706e67)


## 痛点

虽然H5的页面与PC的Web页面相比简单了不少，但让我们头痛的事情是要想尽办法让页面能适配众多不同的终端设备。
看看下图你就会知道，这是多么痛苦的一件事情：


![](https://camo.githubusercontent.com/9598a107e7f7029717f52192c90dcaf7008e49c1/687474703a2f2f7777772e773363706c75732e636f6d2f73697465732f64656661756c742f66696c65732f626c6f67732f323031352f313531312f72656d2d342e706e67)


点击[这里查看](https://design.google.com/devices/)更多终端设备的参数。



再来看看手淘H5要适配的终端设备数据：

![](https://camo.githubusercontent.com/ab4450a21060ca291fc6b7ddc9592c94467d6bd6/687474703a2f2f7777772e773363706c75732e636f6d2f73697465732f64656661756c742f66696c65732f626c6f67732f323031352f313531312f72656d2d372e706e67)



看到这些数据，是否死的心都有了，或者说为此捏了一把汗出来


## 手淘团队适配协作模式


早期移动端开发，对于终端设备适配问题只属于Android系列，只不过很多设计师常常忽略Android适配问题，只出一套iOS平台设计稿。
但随着iPhone6，iPhone6+的出现，从此终端适配问题不再是Android系列了，也从这个时候让移动端适配全面进入到“杂屏”时代。


![](https://camo.githubusercontent.com/0a4ba5a67f639a004a85b371d51d33a737e0f5c8/687474703a2f2f7777772e773363706c75732e636f6d2f73697465732f64656661756c742f66696c65732f626c6f67732f323031352f313531312f72656d2d31312e706e67)

上图来自于 [paintcodeapp.com](http://www.paintcodeapp.com/news/ultimate-guide-to-iphone-resolutions)



为了应对这多么的终端设备，设计师和前端开发之间又应该采用什么协作模式？或许大家对此也非常感兴趣。


而整个手淘设计师和前端开发的适配协作基本思路是：

- 选择一种尺寸作为设计和开发基准
- 定义一套适配规则，自动适配剩下的两种尺寸(其实不仅这两种，你懂的)
- 特殊适配效果给出设计效果


还是上一张图吧，因为一图胜过千言万语：

![](https://camo.githubusercontent.com/8e69ed933a0eff873d4a2b3667461d1e3ec2d790/687474703a2f2f7777772e773363706c75732e636f6d2f73697465732f64656661756c742f66696c65732f626c6f67732f323031352f313531312f72656d2d362e6a7067)



在此也不做更多的阐述。

在手淘的设计师和前端开发协作过程中：

- 手淘设计师常选择iPhone6作为基准设计尺寸，
- 交付给前端的设计尺寸是按750px * 1334px为准(高度会随着内容多少而改变)。
- 前端开发人员通过一套适配规则自动适配到其他的尺寸。
   

根据上面所说的，设计师给我们的设计图是一个750px * 1600px的页面：


![](https://camo.githubusercontent.com/9285fef8a588c2b233f99edacef5c9b3652c2a6e/687474703a2f2f7777772e773363706c75732e636f6d2f73697465732f64656661756c742f66696c65732f626c6f67732f323031352f313531312f72656d2d332e6a7067)



## 前端开发完成终端适配方案

拿到设计师给的设计图之后，剩下的事情是前端开发人员的事了。
而手淘经过多年的摸索和实战，总结了一套移动端适配的方案—— [flexible](https://github.com/amfe/lib-flexible)方案。




这种方案具体在实际开发中如何使用，暂时先卖个关子，在继续详细的开发实施之前，我们要先了解一些基本概念。

### 一些基本概念


在进行具体实战之前，首先得了解下面这些基本概念(术语)：


### 视窗 viewport

简单的理解，viewport是严格等于浏览器的窗口。在桌面浏览器中，viewport就是浏览器窗口的宽度高度。但在移动端设备上就有点复杂。


移动端的viewport太窄，为了能更好为CSS布局服务，所以提供了两个viewport:虚拟的viewportvisualviewport和布局的viewportlayoutviewport。


George Cummins在[Stack Overflow上对这两个基本概念做了详细的解释](http://stackoverflow.com/questions/6333927/difference-between-visual-viewport-and-layout-viewport)。


而事实上viewport是一个很复杂的知识点，上面的简单描述可能无法帮助你更好的理解viewport，而你又想对此做更深的了解，可以[阅读PPK](http://www.w3cplus.com/css/viewports.html)写的相关教程。

###　物理像素(physical pixel)

物理像素又被称为设备像素，他是显示设备中一个最微小的物理部件。
每个像素可以根据操作系统设置自己的颜色和亮度。
正是这些设备像素的微小距离欺骗了我们肉眼看到的图像效果。

![](https://camo.githubusercontent.com/682edd5e2720ae474d4e55b5f329c1080f879a6b/687474703a2f2f7777772e773363706c75732e636f6d2f73697465732f64656661756c742f66696c65732f626c6f67732f3230313231322f726574696e612d7765622d312e6a7067)


### 设备独立像素(density-independent pixel)

设备独立像素也称为密度无关像素，可以认为是计算机坐标系统中的一个点，这个点代表一个可以由程序使用的虚拟像素(比如说CSS像素)，然后由相关系统转换为物理像素。


### CSS像素

CSS像素是一个抽像的单位，主要使用在浏览器上，用来精确度量Web页面上的内容。
一般情况之下，CSS像素称为与设备无关的像素(device-independent pixel)，简称DIPs。


###　屏幕密度


屏幕密度是指一个设备表面上存在的像素数量，它通常以每英寸有多少像素来计算(PPI)


### 设备像素比(device pixel ratio)


设备像素比简称为dpr，其定义了物理像素和设备独立像素的对应关系。它的值可以按下面的公式计算得到：

> 设备像素比 ＝ 物理像素 / 设备独立像素


在JavaScript中，可以通过 `window.devicePixelRatio`获取到当前设备的`dpr`。
而在CSS中，可以通过 `-webkit-device-pixel-ratio`，`-webkit-min-device-pixel-ratio`和 `-webkit-max-device-pixel-ratio`进行媒体查询，
对不同dpr的设备，做一些样式适配(这里只针对webkit内核的浏览器和webview)。


dip或dp,（device independent pixels，设备独立像素）与屏幕密度有关。
dip可以用来辅助区分视网膜设备还是非视网膜设备。

缩合上述的几个概念，用一张图来解释：

![](https://camo.githubusercontent.com/a407f9dc63ca26a60ade9ed8830713c14f6132d8/687474703a2f2f7777772e773363706c75732e636f6d2f73697465732f64656661756c742f66696c65732f626c6f67732f3230313231322f726574696e612d7765622d332e6a7067)


众所周知，iPhone6的设备宽度和高度为 `375pt * 667pt`,可以理解为设备的独立像素；而其dpr为2，根据上面公式，我们可以很轻松得知其物理像素为`750pt * 1334pt`。


如下图所示，某元素的CSS样式：

```
width: 2px;
height: 2px；
```

在不同的屏幕上，CSS像素所呈现的物理尺寸是一致的，而不同的是CSS像素所对应的物理像素具数是不一致的。
在普通屏幕下1个CSS像素对应1个物理像素，而在Retina屏幕下，1个CSS像素对应的却是4个物理像素。


有关于更多的介绍可以点击[这里](http://www.w3cplus.com/css/towards-retina-web.html)详细了解。


看到这里，你能感觉到，在移动端时代屏幕适配除了Layout之外，还要考虑到图片的适配，
因为其直接影响到页面显示质量，对于如何实现图片适配，再此不做过多详细阐述。这里盗用了@南宮瑞揚根据mir.aculo.us翻译的一张信息图：

![](https://camo.githubusercontent.com/55960bfa1419eabdee47efdd2f863a9ab50b3203/687474703a2f2f7777772e773363706c75732e636f6d2f73697465732f64656661756c742f66696c65732f626c6f67732f3230313231322f726574696e612d7765622d31302e6a7067)


### meta标签

`<meta>` 标签有很多种，而这里要着重说的是viewport的meta标签，
其主要用来告诉浏览器如何规范的渲染Web页面，而你则需要告诉它视窗有多大。
在开发移动端页面，我们需要设置meta标签如下：

```
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
```

代码以显示网页的屏幕宽度定义了视窗宽度。网页的比例和最大比例被设置为100%。

留个悬念，因为后面的解决方案中需要重度依赖meta标签。


### CSS单位rem


在 [W3C](http://www.w3.org/TR/css3-values/#rem-unit)规范中是这样描述rem的:

>font size of the root element.

简单的理解，`rem` 就是相对于根元素 `<html>` 的font-size来做计算。
而我们的方案中使用rem单位，是能轻易的根据 `<html>` 的font-size计算出元素的盒模型大小。
而这个特色对我们来说是特别的有益处。






