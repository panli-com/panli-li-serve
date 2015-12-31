title: api.nnn.li 接口说明初始化
date: 2015-12-16 17:59:33
tags:
tags:
  - api
  - nodejs
  - javascript
  - ip
categories:
  - nodejs
---

## 开放接口 

1. http://api.nnn.li/ip/
2. http://api.nnn.li/ip/37.115.98.238

ip/ 				-> 获取当前客户端的 ip 信息
ip/37.115.98.238 	-> 查询指定 ip 的信息


## ajax 调用

```
$.ajax({
        type:"GET",    
        url: "http://api.nnn.li/ip/",
        dataType:"json",
        success:function (result) {
            console.log(JSON.stringify(result));
        },
        error:function (result, status) {
        //处理错误
            console.log(result);
        }
});

```
