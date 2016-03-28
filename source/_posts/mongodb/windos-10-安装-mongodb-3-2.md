title: windos 10 安装 mongodb 3.2
date: 2016-03-28 15:26:14
tags:
  - 数据库
  - mongodb
  - nosql
categories:
  - mongodb
---

## 下载

[官方下载地址](https://www.mongodb.org/downloads?_ga=1.184892399.797153712.1459146001#production)

>Windows 64-bit 2008 R2+

## 安装

- 安装路径  E:\Program Files\MongoDB\Server\3.2\bin
- 设置数据文件路径 E:\Program Files\MongoDB\Server\3.2\data\db
- 设置数据日志文件 E:\Program Files\MongoDB\Server\3.2\data\db\logs.txt


## 配置Mongo服务端

```
E:\Program Files\MongoDB\Server\3.2\bin>
mongod --logpath "E:\Program Files\MongoDB\Server\3.2\data\db\logs.txt" --logappend --dbpath "E:\Program Files\MongoDB\Server\3.2\data\db" --directoryperdb --serviceName "MongoDB" --serviceDisplayName "MongoDB" --install
```

>然后到服务中启 `mongodB` 或者 命令行 `net start MongoDB` (服务名)


## 客户端连接

下载 [Robomongo](https://robomongo.org/download)


## 停止服务

```
E:\Program Files\MongoDB\Server\3.2\bin>net stop MongoDB
MongoDB 服务正在停止.
MongoDB 服务已成功停止。
```