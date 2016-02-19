title: docker管理平台 shipyard 中文版部署
date: 2016-02-18 17:43:48
tags:
  - docker
  - shell
  - 管理平台
  - shipyard
categories:
  - docker
---

## 如何使用 shipyard


### 安装

>自动化安装脚本

```
curl https://nnn.li/docker/deploy | bash -s
```

### 快速删除 shipyard

```
curl https://nnn.li/docker/deploy | ACTION=remove bash -s

```

### 更新升级 shipyard


```
curl https://nnn.li/docker/deploy | ACTION=upgrade bash -s

```

### 增加一个节点

```
curl https://nnn.li/docker/deploy | ACTION=node DISCOVERY=etcd://<你的首次安装主机IP> bash -s
```