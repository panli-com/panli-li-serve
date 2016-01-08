title: Node express项目nginx代理转向绑定域名后 nginx配置获取客户端公网ip
date: 2015-12-16 16:29:51
tags:
  - javascript
  - nodejs
  - nginx
categories:
  - nodejs	
---

## node 代码

```
var express = require('express');
var app = express();
var os = require('os');
var http = require('http');
var cors = require('cors');


app.use(cors());


app.get('/', cors(),function(req, res){  
  var ip = getClientIp(req).match(/\d+\.\d+\.\d+\.\d+/); 
  console.log(ip);
});


function getClientIp(req) {
        return req.headers['x-forwarded-for'] ||
        req.connection.remoteAddress ||
        req.socket.remoteAddress ||
        req.connection.socket.remoteAddress;
}

app.listen(8081);
console.log('listening on port http://localhost:8081/');
```


## nginx 代理

```
server  {
    listen 80;
    server_name nnn.com;
    
    location / {
        proxy_set_header  X-real-IP $remote_addr;
        proxy_pass      http://127.0.0.1:8081;
    }

     access_log  /home/wwwlogs/nnn.com.log  access;
 }
```


直接访问服务器的ip 是正常返回客户端的ip

而访问 nginx 代理转向 的域名地址 返回的ip 却是 127.0.01

nginx 转向的 proxy_pass 地址是多少 ，返回的就是多少

node 如何更好的绑定域名呢？


![](http://sfault-image.b0.upaiyun.com/406/186/4061862233-5670f440a4d08_articlex)


## nginx 解决方案


修改 nginx

```
server  {
    listen 80;
    server_name nnn.com;
    
    location / {
        proxy_pass      http://localhost:8081;
        proxy_redirect off;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_set_header X-NginX-Proxy true;
    }

       access_log  /home/wwwlogs/nnn.com.log  access;
 }
```

## 解构知识

` req.ip `  http://expressjs.com/en/4x/api.html#req.ip

` trust proxy `  http://expressjs.com/en/4x/api.html#trust.proxy.options.table


