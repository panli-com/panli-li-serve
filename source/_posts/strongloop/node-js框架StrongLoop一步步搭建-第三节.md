title: node.js框架StrongLoop一步步搭建 第三节 (LoopBack 数据库配置连接)
date: 2015-10-29 11:21:14
tags:
  - node.js
  - StrongLoop
categories:
  - node
photos:
  - http://zanjs.b0.upaiyun.com/image/3/a0/30b4cfec7a5c0e547153d0ac560e2.png
---

## 配置数据库连接

Loopback 提供了 多种连接数据库的 方案 一下分别是 `命令行` 和 StrongLoop 为我们提供的管理系统

### 命令行方式

- cd 到项目根目录下  `slc loopback:datasource`

> 接下来会进入交互模式

```
? Enter the data-source name: mongodb
? Select the connector for mongodb: MongoDB (supported by StrongLoop)
```

这里我 选了 `mongodb`

下面是选择界面

```
? Enter the data-source name: mysql
? Select the connector for mysql:
  In-memory db (supported by StrongLoop)
  Email (supported by StrongLoop)
> MySQL (supported by StrongLoop)
  PostgreSQL (supported by StrongLoop)
  Oracle (supported by StrongLoop)
  Microsoft SQL (supported by StrongLoop)
  MongoDB (supported by StrongLoop)
(Move up and down to reveal more choices)

```

操作后会在项目目录下的 `server/datasources.json`  文件里增加 我们的 数据源

```
{
  "db": {
    "name": "db",
    "connector": "memory"
  },
  "mongodb": {
    "name": "mongodb",
    "connector": "mongodb"
  }
}
```

在这里 需要我们手动添加 `mongodb` 的连接配置信息 加入 host, port, database, username和password等项

```
{
  "db": {
    "name": "db",
    "connector": "memory"
  },
  "mongodb": {
    "name": "mongodb",
    "connector": "mongodb",
    "host": "127.0.0.1",
    "database": "devDB",
    "username": "devUser",
    "password": "devPassword",
    "port": 27017
  }
}
```

### web在线网页方式
> StrongLoop 为我们提供非常方便的 在线管理您的应用后台

如果您是克隆了 同事的项目 请记得 先全局安装 `npm i -g strongloop`

到我们的项目根目录下 `slc arc` 命令

会自动打开浏览器进入管理界面

```
E:\zan\www\strongloop\loopback\panli-auth>slc arc
Loading workspace E:\zan\www\strongloop\loopback\panli-auth
StrongLoop Arc is running here: http://localhost:24033/#/
```

![loopback login](http://zanjs.b0.upaiyun.com/image/6/73/d4ad7baca1f78490838e4010815f1.png)

这里需要到 [strongloop](https://strongloop.com/register/) 的官网注册一个帐号 才可以登录后台 ，至于为什么，目前还不清楚，很抱歉，哈哈！

注册好后 我们输出帐号登录来到了 非常漂亮的后台

![loopback main page](http://zanjs.b0.upaiyun.com/image/b/a3/73d5f70f710616cbbe6c0216f64db.png)

由于刚才敲入的 是 `mongodb` 的 数据源 所以 在 左侧的 导航 会看到 `Data Sources ` 会有2个数据源
第一个 `db` 表示 内存 一开始项目初始化的时候数据都是存放在 内存中的。
第二个 `mongodb` 是要链接本地mongodb 数据库的 下面是我的配置

![mongodb 数据库](http://zanjs.b0.upaiyun.com/image/3/83/db52891c31449d0d2c964201150ec.png)

点击 `Test Connection 按钮`  如果出现 绿色 的 `Success` 提示 说明 连接数据库成功 ，你可以开心的耍了


如果有不对的地方，请大神 指错， 我也是一边学习 一边 写的 

祝你顺利完成！

(*^__^*) 嘻嘻……
