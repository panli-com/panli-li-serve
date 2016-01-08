title: 同样域名下端口号不一样 ajax 请求ie 浏览器可以而firefox和 谷歌不可以
date: 2015-12-02 17:11:52
tags:
  - javascript
  - ajax
categories:
  - javascript
---

> 端口号不一致在 firefox  和 谷歌 下也算跨域的，而 IE端口不一样不算跨域

## jQuery Ajax 简单的实现跨域请求 demo

>html 代码清单：

```
<script type="text/javascript" src="http://apps.bdimg.com/libs/jquery/1.9.1/jquery.min.js"></script>
<script type="text/javascript">
$(function(){
$.ajax(
    {
        type:'get',
        url : 'http://www.youxiaju.com/validate.php?loginuser=lee&loginpass=123456',
        dataType : 'jsonp',
        jsonp:"jsoncallback",
        success  : function(data) {
            alert("用户名："+ data.user +" 密码："+ data.pass);
        },
        error : function() {
            alert('fail');
        }
    }
);
})
</script>
```


>服务端 validate.php 代码清单：


```
<?php
header('Content-Type:text/html;Charset=utf-8');
$arr = array(
	"user" => $_GET['loginuser'],
	"pass" => $_GET['loginpass'],
	"name" => 'response'

);
echo $_GET['jsoncallback'] . "(".json_encode($arr).")";

```


