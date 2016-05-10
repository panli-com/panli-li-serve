title: ubuntu 16.04 开启root用户ssh登录
date: 2016-05-10 10:06:58
tags:
   - ubuntu
   - ssh
   - root
categories:
  - linux  
---

## 修改 root 密码

```
sudo passwd root
```

## 修改ssh 配置文件

以其他账户登录，通过 `sudo vi` 修改 `/etc/ssh/sshd_config`
```
z@zans:~$ su
密码： 
root@zans:/home/z# vi /etc/ssh/sshd_config
```

找到以下内容区域

```
# Authentication:
LoginGraceTime 120
#PermitRootLogin prohibit-password
PermitRootLogin yes
StrictModes yes
```

注释掉 #PermitRootLogin prohibit-password

添加 PermitRootLogin yes


## 重启 ssh 服务

```
root@zans:/home/z# /etc/init.d/ssh restart
[ ok ] Restarting ssh (via systemctl): ssh.service.
```
