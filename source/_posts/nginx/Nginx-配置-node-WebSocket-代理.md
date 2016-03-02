title: Nginx 配置 node WebSocket 代理
date: 2016-02-25 12:57:24
tags:
  - node.js
  - WebSocket
  - Nginx
categories:
  - Nginx
---

在用 `node.js ` 开发` WebSocket` 应用的时候,直接访问 端口号 WebSocket 是正常握手成功的,
但配了  Nginx 代理的  时候,握手却失败

最后配置如下 握手成功 

```
server {
        listen       80;
        server_name  lg.in;
        
        location / {		
            proxy_pass	  http://127.0.0.1:4567/;
            proxy_redirect off;
            
            proxy_http_version 1.1;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header Host $http_host;
            proxy_set_header X-NginX-Proxy true;       
            
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
      }
      
}

```

> 关键点 就是  `header` 对应的 `Upgrade`

具体 HTTP Header 上的参数参考 SegmengFault 上的文章: 
http://segmentfault.com/a/1190000000382788