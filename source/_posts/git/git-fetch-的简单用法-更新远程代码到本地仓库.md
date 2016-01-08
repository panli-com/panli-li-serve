title: 'git fetch 的简单用法:更新远程代码到本地仓库'
date: 2015-12-28 15:17:40
tags:
  - git
categories:
  - 管理工具 
---

## 查看远程仓库 

>git remote -v

```
$ git remote -v
origin  git@github.com:zanjs/ippt.git (fetch)
origin  git@github.com:zanjs/ippt.git (push)

```


从上面的结果可以看出，远程仓库有一个 origin


##　从远程获取最新版本到本地

>git fetch origin master

```
$ git fetch origin master
remote: Counting objects: 17, done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 17 (delta 11), reused 15 (delta 9), pack-reused 0
Unpacking objects: 100% (17/17), done.
From github.com:zanjs/ippt
 * branch            master     -> FETCH_HEAD
   7c6a6db..8dafd85  master     -> origin/master

```


$ git fetch origin master 这句的意思是：
从远程的origin仓库的master分支下载代码到本地的origin master


## 比较本地的仓库和远程参考的区别 

>git log -p master.. origin/master


```
$ git log -p master.. origin/master
commit 8dafd85f249f1d20275052a402657a746a51111c
Author: zanjs <root@zanjs.com>
Date:   Sat Dec 26 13:37:42 2015 +0800

    ippt By gitpush

diff --git a/package.json b/package.json
index 21aac2b..43523a8 100644
--- a/package.json
+++ b/package.json
@@ -1,6 +1,6 @@
 {
   "name": "ippt",
-  "version": "0.0.7",
+  "version": "0.0.8",
   "description": "ppt,nodejs,javascript",
   "main": "./bin/ippt",
   "bin": { "ppt": "./bin/ippt" },

commit 8ea5978c749b71eace036f6ba05424e24b947e6b
Author: zanjs <root@zanjs.com>
Date:   Sat Dec 26 13:36:02 2015 +0800

:
```

我的本地代码和远程代码不相同,由于是在2台电脑上做了提交

## 把远程下载下来的代码合并到本地仓库，远程的和本地的合并

>git merge origin/master

```
Administrator@WIN-9PH4ISN44NM MINGW64 /e/zan/coding/panli/ppt/ippt (master)
$ git merge origin/master
Updating 7c6a6db..8dafd85
Fast-forward
 assets/js/nodeppt.js  |  4 ++--
 bin/{ippt.js => ippt} |  0
 lib/server.js         | 12 ++++++------
 package.json          |  8 ++++----
 template/markdown.ejs |  2 +-
 up.md                 |  8 ++++++++
 6 files changed, 21 insertions(+), 13 deletions(-)
 rename bin/{ippt.js => ippt} (100%)
 create mode 100644 up.md

```
由于远程的是最新的 所以需要更新我本地的代码

