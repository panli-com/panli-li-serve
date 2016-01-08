title: node.js框架StrongLoop一步步搭建 第一节 (LoopBack run)
date: 2015-10-29 09:00:39
tags:
  - node.js
  - StrongLoop
categories:
  - node
photos:
  - http://zanjs.b0.upaiyun.com/image/3/a0/30b4cfec7a5c0e547153d0ac560e2.png
---

## Install StrongLoop 安装到全局

``` bash
$ npm install -g strongloop
```

##  Create app 创建一个应用
> Create a "Hello World" LoopBack application.

> 创建一个 “Hello World” 的 LoopBack 应用

``` bash
$ slc loopback
[?] Enter a directory name where to create the project: hello-world
[?] What\'s the name of your application? hello-world
```
<!--more-->

## Create models 为应用创建一个模型

```
$ cd hello-world
$ slc loopback:model
```


接下来会交互 模型的 值 按照您的需求输入

```
[?] Enter the model name: person
[?] Select the data-source to attach person to: db (memory)
[?] Expose person via the REST API? Yes
[?] Custom plural form (used to build REST URL): people
Let's add some person properties now.
```

创建模型的字段名称

 ```
Enter an empty property name when done.
[?] Property name: firstname
 ```

 选择字段类型 上下键切换

 ```
 [?] Property type: (Use arrow keys)
❯ string
  number
  boolean
  object
  array
  date
  buffer
  geopoint
  (other)
 ```

 是否是必填 默认为 N

```
 [?] Required? (y/N) y
```

##  Run the application 运行 这个应用

```
$ node .
Browse your REST API at http://0.0.0.0:3000/explorer
Web server listening at: http://0.0.0.0:3000/
```

浏览器打开 http://localhost:3000/explorer

就可以看到 所有 http 请求的 api 接口 ,这里提供了很方便的测试，棒棒的
