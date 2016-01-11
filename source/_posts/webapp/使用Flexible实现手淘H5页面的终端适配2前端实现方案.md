title: 使用Flexible实现手淘H5页面的终端适配 笔记之(2)前端实现方案
date: 2016-01-08 11:49:36
tags:
 - webapp
 - mobile
 - h5
 - Flexible
 - 终端适配
categories:
  - mobile
---

## 前端实现方案


了解了前面一些相关概念之后，接下来我们来看实际解决方案。
在整个手淘团队，我们有一个名叫 [lib-flexible](https://github.com/amfe/lib-flexible)的库，而这个库就是用来解决H5页面终端适配的。

### lib-flexible是什么？

[lib-flexible](https://github.com/amfe/lib-flexible) 是一个制作H5适配的开源库。


当然你可以直接使用阿里CDN：

```
<script src="http://g.tbcdn.cn/mtb/lib-flexible/{{version}}/??flexible_css.js,flexible.js"></script>
```

将代码中的 `{{version}}`换成对应的版本号0.3.4。


### 使用方法

lib-flexible库的使用方法非常的简单，只需要在Web页面的 `<head></head>` 中添加对应的flexible_css.js,flexible.js文件：