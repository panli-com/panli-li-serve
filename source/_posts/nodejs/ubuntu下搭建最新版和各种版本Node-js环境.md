title: ubuntu下搭建最新版和各种版本Node.js环境
date: 2016-02-17 14:43:31
tags:
tags:
  - node.js
  - ubuntu
  - node
categories:
  - node
---

## nvm安装 nodejs

### 获取nvm

```bash
root@iZ28krk4xlkZ:/home/git/node#   git clone https://github.com/creationix/nvm.git
Cloning into 'nvm'...
remote: Counting objects: 4399, done.
remote: Compressing objects: 100% (20/20), done.
remote: Total 4399 (delta 4), reused 0 (delta 0), pack-reused 4379
Receiving objects: 100% (4399/4399), 1.11 MiB | 23.00 KiB/s, done.
Resolving deltas: 100% (2578/2578), done.
Checking connectivity... done.
```


### 安装nvm


- 下载之后，进入目录直行 `./install.sh`
- 安装之后输入 `nvm` 还是提示没有这时候需要直行 `source ./nvm.sh`


> 将 `source /root/nvm/nvm.sh` 写入 `~/.bashrc` 或者其启动脚本中，
> 这样在系统启动的时候会自动执行这条指令。
> 开机就可以使用 `nvm` 了；


```
root@iZ28krk4xlkZ:/home/git/node# ls
nvm
root@iZ28krk4xlkZ:/home/git/node# cd nvm/
root@iZ28krk4xlkZ:/home/git/node/nvm# ls
bash_completion  CONTRIBUTING.md  install.sh  LICENSE.md  Makefile  nvm-exec  nvm.sh  package.json  README.markdown  test
root@iZ28krk4xlkZ:/home/git/node/nvm# ./install.sh 
=> Downloading nvm from git to '/root/.nvm'
=> Cloning into '/root/.nvm'...
remote: Counting objects: 4399, done.
remote: Compressing objects: 100% (20/20), done.
remote: Total 4399 (delta 4), reused 0 (delta 0), pack-reused 4379
Receiving objects: 100% (4399/4399), 1.11 MiB | 15.00 KiB/s, done.
Resolving deltas: 100% (2578/2578), done.
Checking connectivity... done.
* (detached from v0.31.0)
  master

=> Appending source string to /root/.bashrc
=> Close and reopen your terminal to start using nvm
root@iZ28krk4xlkZ:/home/git/node/nvm# source ./nvm.sh
```

### nvm安装任意版本nodejs

- 通过nvm ls查看当前已经安装的node或者iojs版本

- 通过nvm ls-remote查看当前可以安装的node或者iojs版本

- 通过nvm install 5.6.0 安装制定版本的nodejs

- 通过nvm use 5.6.0 切换使用的nodejs版本


nvm install 5.0.0 

```

root@iZ28krk4xlkZ:/home/git/node/nvm# nvm install 5.0.0
Downloading https://nodejs.org/dist/v5.0.0/node-v5.0.0-linux-x64.tar.xz...
#####                                                                      8.1%
curl: (56) SSL read: error:00000000:lib(0):func(0):reason(0), errno 104
Binary download failed, trying source.
######################################################################## 100.0%
Checksums empty
Now using node v5.0.0 (npm v3.3.6)
Creating default alias: default -> 5.0.0 (-> v5.0.0)
root@iZ28krk4xlkZ:/home/git/node/nvm# node -v
v5.0.0

```


###  nvm基本用法


```
  nvm help：显示帮助信息
  nvm --version：查看当前版本
  nvm install [-s] <version>：下载安装nodejs/iojs  
  nvm uninstall <version>：卸载安装nodejs/iojs 
  nvm use <version> ：切换 nodejs/iojs 版本
  nvm ls：列出当前已安装的 nodejs/iojs                
  nvm ls-remote：列出当前可安装的nodejs/iojs
```


[nvm详细文档](https://github.com/creationix/nvm)




