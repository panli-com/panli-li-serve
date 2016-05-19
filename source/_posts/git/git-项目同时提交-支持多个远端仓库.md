title: git 项目同时提交 支持多个远端仓库
date: 2016-05-19 13:40:21
tags:
  - git
categories:
  - 管理工具
  - git
---

github 的代码管理 无疑是最棒的, 但有时候，我们需要同时提交到 自己公司的 git 代码管理平台

下面我们就来 给自己的 git 项目 添加 多个 远程 仓库

## add 

给自己的项目 添加 一个仓库

```
git remote add panli http://github.panli.com/React/React.git
```

## push

```
git push panli
```