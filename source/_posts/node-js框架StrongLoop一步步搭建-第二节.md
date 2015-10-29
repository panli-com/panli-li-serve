title: node.js框架StrongLoop一步步搭建 第二节 (LoopBack 安装数据库)
date: 2015-10-29 10:43:08
tags:
  - node.js
  - StrongLoop
categories:
  - node
photos:
  - http://zanjs.b0.upaiyun.com/image/3/a0/30b4cfec7a5c0e547153d0ac560e2.png
---

## 安装数据库驱动

LoopBack 不是所有的事情都帮你做了，你还需要手动安装一下你需要的数据库

目前 LoopBack 支持如下数据库:

mongodb
```
$ npm install loopback-connector-mongodb --save
```
出处详情
https://docs.strongloop.com/display/public/LB/MongoDB+connector

mysql
```
$ npm install loopback-connector-mysql --save
```
出处详情
https://docs.strongloop.com/display/public/LB/MySQL+connector

oracle
```
$ npm install loopback-connector-oracle --save
```
出处详情
https://docs.strongloop.com/display/public/LB/Oracle+connector

postgresql

```
$ npm install loopback-connector-postgresql --save
```
出处详情
https://docs.strongloop.com/display/public/LB/PostgreSQL+connector


SQL+Server

```
$ npm install loopback-connector-mssql --save
```
出处详情
https://docs.strongloop.com/display/public/LB/SQL+Server+connector
