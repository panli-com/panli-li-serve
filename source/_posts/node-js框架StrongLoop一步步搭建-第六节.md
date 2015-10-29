title: node.js框架StrongLoop一步步搭建 第六节 (loopback 插入数据库(mongodb))
date: 2015-10-29 16:10:00
tags:
  - node.js
  - StrongLoop
  - loopback
categories:
  - node
photos:
  - http://zanjs.b0.upaiyun.com/image/3/a0/30b4cfec7a5c0e547153d0ac560e2.png
---

## loopback 插入数据库
>mongodb 篇

上几节相信大家的项目都可以运行起来了,下面就开始 玩玩 mongodb 这个家伙吧

在玩之前希望测试一下是否已经 连接到 `mongodb`

 可以登录 启动 StrongLoop 的 api 平台

 ```
 $ slc arc
 ```

 ![StrongLoop api 平台](http://zanjs.b0.upaiyun.com/image/9/6c/b4c228b5d0bb089ad8f83cbfbae94.png)

 >点击 大大的按钮 看到 Success 就正常已经正常连接到 mongodb 了

###  配置 datasources.json  内容如下
> 根据您 mongodb 的 配置 填入

```
{
  "db": {
    "name": "db",
    "connector": "memory"
  },
  "mongodb": {
    "host": "127.0.0.1",
    "port": 27017,
    "password": "",
    "name": "mongodb",
    "connector": "mongodb",
    "url": "mongodb://localhost:27017/panli-auth",
    "user": ""
  }
}

```

### 配置 model-config.json

>这里我吧 `dataSource` 都改成了 'mongodb'  

>mongodb 的数据源 在 datasources.json 的文件里配置好了 上面已经配置了

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
  "AccessToken": {
    "dataSource": "mongodb",
    "public": false
  },
  "ACL": {
    "dataSource": "mongodb",
    "public": false
  },
  "RoleMapping": {
    "dataSource": "mongodb",
    "public": false
  },
  "Role": {
    "dataSource": "mongodb",
    "public": false
  },
  "PanUser": {
    "dataSource": "mongodb",
    "public": true
  }
}

```

### scl run 运行应用

```
E:\zan\www\strongloop\loopback\panli-auth>slc run
INFO strong-agent v2.0.2 profiling app 'panli-auth' pid '7752'
INFO strong-agent[7752] started profiling agent
INFO supervisor reporting metrics to `internal:`
supervisor running without clustering (unsupervised)
Swagger: skipping unknown type "ObjectID".
Web server listening at: http://localhost:3000
Browse your REST API at http://localhost:3000/explorer

```

浏览器打开 http://localhost:3000/explorer

在这里 我们可以测试接口的数据

下面演示一下

![api gif](http://zanjs.b0.upaiyun.com/image/f/0c/f07b3315a75d8f13ff07e21b6dd8b.gif)


>上面是演示注册用户的api 接口 post 提交 http://localhost:3000/api/users

在文本框内输入三个必填项 username ， email 和 password

```
{
"username":"za2",
"email":"zz@z2.com",
"password":"qq123"
}
```

提交后 在下面的 Response Body 可以看到 我们注册的用户信息了

```
{
  "username": "za2",
  "email": "zz@z2.com",
  "id": "5631dc4d59ab85481e474aec"
}
```

看到 id 的键值 就可以知道 他插入到了 mongodb 了


我还是不相信我的眼睛 ， 吓得我 跑到 mongodb 瞧一瞧 嘻嘻！

```
> show dbs
local       0.078GB
panli-auth  0.078GB
test        0.078GB
> use panli-auth
switched to db panli-auth
> show tables
PanUser
system.indexes
> show collections
PanUser
system.indexes
> db.PanUser.find()
{ "_id" : ObjectId("5631d38859ab85481e474aeb"), "username" : "za", "password" :
"$2a$10$OnuNv/YTPSYzYUi9S9UJ3eArmRmZQbRCyBnqt6xxozYEjSMIE2PTK", "email" : "zz@z.
com" }
{ "_id" : ObjectId("5631dc4d59ab85481e474aec"), "username" : "za2", "password" :
 "$2a$10$9q5X4y570Ti3SdfMg4ANr.dHOdjZpPW3.JOxE5GB2U6t9XCngZyVq", "email" : "zz@z
2.com" }
>
```

可以看到 数据以及躺在 mongodb 里啦

如果有不对的地方，请大神 指错， 我也是一边学习 一边 写的
