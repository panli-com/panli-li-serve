title: 双系统下Linux（ubuntu）不能进入windows的NTFS分区之挂载错误问题解决
date: 2016-04-06 10:43:32
tags:
  - linux
  - ubuntu
categories:
  - linux
---


### 问题 不能访问

安装完ubuntu后，不能访问win10里面的分区，
访问会提示不能访问XXX ，Error mounting /dev/sda8 at /media/my/XXX: Command-line `mount -t "ntfs" -o

### 解决办法

1、打开终端：如果没有安装ntfs-3g就要安装：`sudo apt-get install ntfs-3g`
2、修复挂载错误的相应的分区如提示中的/dev/sda5，输入：
```
sudo ntfsfix /dev/sda5
```
回车就可以了。


### 解决办法2


进入window系统设置------控制面板-----电源选项--------

左侧项目栏“选择电源按钮的功能”或者“选择关闭盖子的功能”-----

“更改当前不可用的设置”来 把下面的启动快速启动 去掉选择
