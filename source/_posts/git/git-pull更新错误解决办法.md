title: ' git pull更新错误解决办法'
date: 2016-05-10 15:54:30
tags:
  - git
categories:
  - 管理工具
  - git
---

## git pull error

```
Your local changes to the following files would be overwritten by merge
error: Your local changes to the following files would be overwritten by merge:
```

## 保存更改

```
git stash
git pull
git stash pop
```
然后可以使用git diff -w +文件名 来确认代码自动合并的情况.

## 完全覆盖本地工作

```
git reset --hard
git pull
```
其中git reset是针对版本

