title: Phantomjs 笔记 安装配置 1
date: 2016-07-08 10:01:19
tags:
  - node.js
  - network
  - phantomjs
categories:
  - nodejs
---

## Phantomjs install

幻影幽灵 Js （名字好霸气呀）

[Phantomjs官网](http://phantomjs.org/)

### npm install

npm 安装是最简单快捷的方案

```
npm install -g phantomjs
```

### Download

[下载地址](http://phantomjs.org/download.html)

去 [phantomjs](http://phantomjs.org/download.html)) 官网 下载 各个平台的包


### OS 系统环境


在OSX和Linux上分别可以通过 `Homebrew` 和 `yum`（或 `apt-get` ）安装

```
//osx
brew phantomjs
// centos
yum install phantomjs
// ubuntu
apt-get install phantomjs
```

Windows上则可以 [phantomjs](http://phantomjs.org/download.html)) 官网 直接下载release包，
解压后放置到合适的目录下，然后环境变量中增加bin文件夹的目录即可


无论是OSX、Linux还是Windows，配置完成后执行phantomjs -v，
如果没有报错并打印出了对应的版本号，
就证明安装配置成功了，否则就需要检查一下是哪里出现了问题。