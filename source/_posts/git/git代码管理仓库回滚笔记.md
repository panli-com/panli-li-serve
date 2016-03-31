title: git代码管理仓库回滚笔记
date: 2016-03-29 15:52:06
tags:
  - git
categories:
  - 管理工具
  - git
---

>git代码库回滚: 指的是将代码库某分支退回到以前的某个commit id

## 本地代码库回滚


- `git reset --hard commit-id` :回滚到commit-id，讲commit-id之后提交的commit都去除

- `git reset --hard HEAD~3` ：将最近3次的提交回滚


## 远程代码库回滚

> 这个是重点要说的内容，过程比本地回滚要复杂

> 应用场景：自动部署系统发布后发现问题，需要回滚到某一个commit，再重新发布


> 原理：先将本地分支退回到某个commit，删除远程分支，再重新push本地分支


### 操作步骤：

1. `git checkout dev`

2. `git pull`

3. `git branch dev_backup` //备份一下这个分支当前的情况

4. `git reset --hard the_commit_id` //把dev本地回滚到the_commit_id

5. `git push origin :dev` //删除远程 dev

6. git push origin dev  //用回滚后的本地分支重新建立远程分支

7. git push origin :dev_backup //如果前面都成功了，删除这个备份分支


> 如果使用了gerrit做远程代码中心库和code review平台，
> 需要确保操作git的用户具备分支的push权限，
> 并且选择了 Force Push选项（在push权限设置里有这个选项）

> 另外，gerrit中心库是个bare库，将HEAD默认指向了master，
> 因此master分支是不能进行删除操作的，最好不要选择删除master分支的策略，换用其他分支。
> 如果一定要这样做，可以考虑到gerrit服务器上修改HEAD指针。。。不建议这样搞


参考资料：https://review.typo3.org/Documentation/access-control.html#category_push
