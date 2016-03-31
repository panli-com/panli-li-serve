title: Ubuntu 14.04 安装MongoDB社区版
date: 2016-03-31 13:48:38
tags:
  - 数据库
  - mongodb
  - nosql
categories:
  - mongodb
---

## 安装MongoDB社区版

1. 通过Ubuntu的包管理系统导入MongoDB的公共密钥

```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
```

2. 创建一个MongoDB软件源的列表文件


创建 `/etc/apt/sources.list.d/mongodb-org-3.2.list` 空文件.


例如：

```
vi /etc/apt/sources.list.d/mongodb-org-3.2.list
```

Ubuntu 12.04 在终端下执行：

```
echo "deb http://repo.mongodb.org/apt/ubuntu precise/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
```

Ubuntu 14.04 在终端下执行：

```
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
```

将软件源加入到刚创建的空文件中。

3. 重新加载本地软件包数据库

```
sudo apt-get update
```

4. 安装MongoDB包

你可以安装最新的稳定版本的MongoDB，也可以安装指定版本的MongoDB

安装最新的稳定版本的MongoDB

终端下执行如下命令：


```
sudo apt-get install -y mongodb-org
```

安装指定版本的MongoDB发行包

为了安装指定的发行包，你需要指定要安装的每一个组件包的名称和版本。 

例如：

```
sudo apt-get install -y mongodb-org=3.2.1 mongodb-org-server=3.2.1 mongodb-org-shell=3.2.1 mongodb-org-mongos=3.2.1 mongodb-org-tools=3.2.1
```

> 如果你只安装 mongodb-org=3.2.1 而没有指定组件包，MongoDB最新版本的每一个包都会被安装，不管你指定的版本是什么。


锁定MongoDB的版本


Ubuntu下会通过 `apt-get` 命令自动升级MongoDB的版本。为了阻止这样，需要锁定已安装MongoDB的版本。顺序执行如下命令即可：


```
echo "mongodb-org hold" | sudo dpkg --set-selections
echo "mongodb-org-server hold" | sudo dpkg --set-selections
echo "mongodb-org-shell hold" | sudo dpkg --set-selections
echo "mongodb-org-mongos hold" | sudo dpkg --set-selections
echo "mongodb-org-tools hold" | sudo dpkg --set-selections
```

5. 启动MongoDB社区版

>安装好MongoDB后，数据库服务应该会自动启动。


默认配置下，MongoDB 数据文件 存储在 `/var/lib/mongodb`，日志文件 存储在 `/var/log/mongodb`，使用 mongodb 账号运行。你可以通过修改


`/etc/mongod.conf` 指定日志和数据文件的存放位置。


5.1 启动MongoDB

终端下执行如下命令启动mongod

```
sudo service mongod start
```

5.2 验证MongoDB已经成功启动

查看 /var/log/mongodb/mongod.log日志文件来验证是否已正确启动，文件如果出现：

```
[initandlisten] waiting for connections on port <port>
```


表明启动成功。


```
<port>是mongoDB鉴定的端口号，在文件/etc/mongod.conf配置，27017 是默认值。
```

5.3 停止MongoDB

```
sudo service mongod stop
```

5.4 重启MongoDB


```
sudo service mongod restart
```


6. 卸载MongoDB社区版


完整地从系统中卸载MongoDB，必须 

    - 通过MongoDB的卸载命令卸载应用程序 
    - 删除MongoDB配置文件 
    - 删除任何包含属于MongoDB的数据和日志
    > 卸载是不可恢复的，请事先做好相关备份工作！
    
6.1 停止MongoDB
    
```
sudo service mongd stop
```
        
6.2 删除包
    
```
sudo apt-get purge mongodb-org*
```
        
6.3 删除数据文件夹
    
```
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb
```
        
7. 可能遇到的麻烦


```
在导入MongoDB软件源证书还有下载MongoDB时出现无法连接情况，那么换个网络环境 试试了！
```
    
    
    
    

