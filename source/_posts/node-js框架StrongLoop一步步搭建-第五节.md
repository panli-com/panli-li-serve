title: node.js框架StrongLoop一步步搭建 第五节 (LoopBack 模型(model)属性添加)
date: 2015-10-29 15:10:28
tags:
  - node.js
  - StrongLoop
  - loopback
categories:
  - node
photos:
  - http://zanjs.b0.upaiyun.com/image/3/a0/30b4cfec7a5c0e547153d0ac560e2.png
---

## 模型(model)添加新属性

### 命令行方式

- cd 到项目根目录下  `slc loopback:property`

选择属性添加到哪个模型里 - 我选择了上节创建的 `PanUser` 模型

```
E:\zan\www\strongloop\loopback\panli-auth>slc loopback:property
? Select the model:
  Change
  Checkpoint
  Email
> PanUser
  Role
  RoleMapping
  Scope
(Move up and down to reveal more choices)
```

要添加属性的名称 输入 `age` 选择 number 字段类型

```
? Select the model: PanUser
? Enter the property name: age
? Property type:
  string
> number
  boolean
  object
  array
  date
  buffer
(Move up and down to reveal more choices)
```

是否必填 输入 N

```
? Select the model: PanUser
? Enter the property name: age
? Property type: number
? Required? No
```

到此  为 模型(model)添加新属性 结束

### web在线网页方式

忽视吧 哈哈...

StrongLoop API平台 傻瓜式操作 

>如果有不对的地方，请大神 指错， 我也是一边学习 一边 写的
