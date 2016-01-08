title: node.js框架StrongLoop一步步搭建 第四节 (LoopBack 模型(model)的创建)
date: 2015-10-29 14:15:11
tags:
  - node.js
  - StrongLoop
categories:
  - node
photos:
  - http://zanjs.b0.upaiyun.com/image/3/a0/30b4cfec7a5c0e547153d0ac560e2.png
---



## 创建新模型(model)

如果您还在停留在手工创建 模型(model)，是不是感觉很不爽 ！
是的，`StrongLoop` 给我们带来的更加规范的模式！下面进入正题

### 命令行方式

- cd 到项目根目录下  `slc loopback:model`

> 接下来会进入交互模式

这里是输入模型名称 我输入了 `PanUser` (我理解为数据库的表名！！ 惭愧了 (*^__^*) 嘻嘻……)

```
? Enter the model name: PanUser
```
下面选择 模型(model) 的 存放数据源， 由于在前面我已经创建了 mongodb 的数据源 (为数据持久化)

如果您还没有创建数据源的话，可能选项只有 一个 `db (memory)` 存放在内存中

这里我选择了 mongodb (mongodb) 第二个选择

```
? Select the data-source to attach PanUser to:
  (no data-source)
> db (memory)
  mongodb (mongodb)

```

接下来我们要选择 模型继承类 ，这里我们想建立一个用户系统，
`PanUser` 这个模型 继续 loopback 自身内建的 `User` 类
一直下拉 选择 `User` 回车

```
? Enter the model name: PanUser
? Select the data-source to attach PanUser to: mongodb (mongodb)
? Select model's base class (Use arrow keys)
  Model
> PersistedModel
  ACL
  AccessToken
  Application
  Change
  Checkpoint
(Move up and down to reveal more choices)

```

回车后我们看到了 如下

```
? Enter the model name: PanUser
? Select the data-source to attach PanUser to: mongodb (mongodb)
? Select model's base class User
? Expose PanUser via the REST API? (Y/n) -- Y键回车 暴露这个接口
```

下面填写 REST 接口 的 url 地址 -- 我填写了 users
```
? Enter the model name: PanUser
? Select the data-source to attach PanUser to: mongodb (mongodb)
? Select model's base class User
? Expose PanUser via the REST API? Yes
? Custom plural form (used to build REST URL): users
```

主要配置都完成了 当输入完 REST 接口 的 url 地址 回车后，
就该添加字段了 ,由于 `PanUser` 已经继承了 loopback 的 `User`
所以 一些该有的字段 都已经有了 例如 username email password 等等
这里我输入了 `fullname`

```
E:\zan\www\strongloop\loopback\panli-auth>slc loopback:model
? Enter the model name: PanUser
? Select the data-source to attach PanUser to: mongodb (mongodb)
? Select model's base class User
? Expose PanUser via the REST API? Yes
? Custom plural form (used to build REST URL): users
Let's add some PanUser properties now.

Enter an empty property name when done.
? Property name: fullname
```

选择 字段类型 'string'

```
Enter an empty property name when done.
? Property name: fullname
(!) generator#invoke() is deprecated. Use generator#composeWith() - see http:
eoman.io/authoring/composability.html
   invoke   loopback:property
? Property type: (Use arrow keys)
> string
  number
  boolean
  object
  array
  date
  buffer
(Move up and down to reveal more choices)
```

是否必填  no

```
? Property type: string
? Required? No

Let's add another PanUser property.
Enter an empty property name when done.
? Property name:
```

接下来会继续增加字段 这里就不增加了 按下 ctrl+c 退出交互

有人会问 以上命令都做了哪些 设置呢？

在项目根目录下 多了 一个 common 文件夹 结构如下

![common](http://zanjs.b0.upaiyun.com/image/6/bd/d24478084298afc75a0ece6bd7712.png)


可以看到 models 增加了 2个文件 `pan-user.js` 和 `pan-user.json`

pan-user.js 可以写入我们的业务逻辑

pan-user.json 是模型配置参数

还有一个地方做了修改 在 server/model-config.json 下  可以看到 增加了如下配置

```
{
  "_meta": {
    "sources": [
      "loopback/common/models",
      "loopback/server/models",
      "../common/models",
      "./models"
    ],
    "mixins": [
      "loopback/common/mixins",
      "loopback/server/mixins",
      "../common/mixins",
      "./mixins"
    ]
  },
  "User": {
    "dataSource": "db"
  },
  "AccessToken": {
    "dataSource": "db",
    "public": false
  },
  "ACL": {
    "dataSource": "db",
    "public": false
  },
  "RoleMapping": {
    "dataSource": "db",
    "public": false
  },
  "Role": {
    "dataSource": "db",
    "public": false
  },
  "PanUser": {
    "dataSource": "mongodb",
    "public": true
  }
}
```
在最后面 增加 了 `PanUser`;
这个在 我们手工 写入 `model` 时 是不能忘记的


### web在线网页方式
> 如果您看过了 第三季的 话， 我想这里就很简单了
> 如果您没有看,可以看一下上一节的 操作

![model](http://zanjs.b0.upaiyun.com/image/2/a5/1d82a29ecfb182ac919b8d578e07d.png)

可以看到 这里已经显示了 刚才 我们用命令行的方式 添加的 `PanUser`

这里都是傻瓜式操作了，大家自己玩玩吧！ `O(∩_∩)O哈哈`

如果有不对的地方，请大神 指错， 我也是一边学习 一边 写的
