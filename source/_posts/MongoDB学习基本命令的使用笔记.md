title: MongoDB学习基本命令的使用笔记
date: 2015-11-10 13:58:49
tags:
  - 数据库
  - mongodb
  - nosql
categories:
  - mongodb
---

## 基础块

### Help查看命令提示

```
  db.help();

  db.yourColl.help();

  db.youColl.find().help();

  rs.help();
```

### 查询所有数据库

```
 show dbs;
```

### 切换/创建数据库

>  当创建一个集合(table)的时候会自动创建当前数据库

```
use DBName;
```

### 查看当前使用的数据库

```
 db.getName();
 
 db;
```

### 显示数据库列表 

```
show dbs;
```

### 显示当前数据库中的集合（类似关系数据库中的表）

```
show collections;
```

### 显示用户

```
show users;
```

### 从指定主机上克隆数据库

>将指定机器上的数据库的数据克隆到当前数据库

```
db.cloneDatabase(“127.0.0.1”); 
```

### 从指定的机器上复制指定数据库数据到某个数据库

>将本机的mydb的数据复制到temp数据库中

```
db.copyDatabase("mydb", "temp", "127.0.0.1");
```

### 删除当前使用数据库

```
db.dropDatabase();
```

### 修复当前数据库

```
 db.repairDatabase();
```

> db和getName方法是一样的效果，都可以查询当前使用的数据库

### 显示当前db状态

```
db.stats();
```

### 当前db版本

```
 db.version();
```

### 查看当前db的链接机器地址

```
 db.getMongo();
```