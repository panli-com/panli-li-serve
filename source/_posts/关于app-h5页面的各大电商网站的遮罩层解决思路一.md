title: 关于app h5页面的各大电商网站的遮罩层解决思路一
date: 2015-12-17 14:06:19
tags:
  - app
  - mobile
  - h5
  - ip
categories:
  - mobile
---

## 需求展现举例

> H5 嵌入 天猫商品详细页

![](http://zanjs.b0.upaiyun.com/image/c/1a/841e4608c6989cf394e5b1ca98a5b.png)

> 加入遮罩层后

![](http://zanjs.b0.upaiyun.com/image/0/b0/5a5f70af00a683037b9a5950e4c3a.png)

> 加入遮罩层后参数说明

![](http://zanjs.b0.upaiyun.com/image/2/03/2d4b0f88ce78231be4b243aafaf93.png)


## 参数指南

>到这里 我们可以看到 遮罩层有 `2` 类 ;

分别是: ** maskTop('顶部遮罩层') ** 、** maskBottom('底部遮罩层') **;

每个遮罩层分别有 **height('高度')** 、**backgroundColor('背景颜色')**


** maskTop('顶部遮罩层') **  有 **top('距离顶部位置')**

** maskBottom('底部遮罩层') ** 有 **bottom('距离低部位置')**

## 各大电商网站布局的不同

> 介于形形色色的电商网站的布局有所不同 , 所以需要我们分别设置 各个网站遮罩层的 **参数**

## 遮罩层的参数灵活化

> 为了可以更好的管理 遮罩层的参数位置和显现样式，一切都有后台添加设置

## demo的数据演示

如下代码可以看到:

`tmall.com` 和 `taobao.com` ** 2 ** 个网站的 遮罩层的参数

由于在挂国外ip vpn代理访问 天猫页面的时候,天猫网站做了页面导向,以致页面布局发生了变动, 
从而导致页面遮罩层的错误，所以做了 `china` 和 `noChina` 的 布局参数

`china` 和 `noChina ` 下面的 参数说明：

- `topMask`    对应的是 ** maskTop('顶部遮罩层') ** 
- `bottomMask` 对应的是 ** maskBottom('底部遮罩层') **

最后可以看到还有一个 `status` 参数：

- `status` 意为是否启用 `noChina` 0 为启用 ; 若不启用 可以填写其它字符


> 以下字段必须全部填写， 如果 `status` 字段为 非 0 , `noChina`对象 可以无


```
var fixedLib = {	
	'tmall.com':{
		'status':0,
		'china':{
			'topMask':{
				'top':'40px',
				'height':'50px',
				'backgroundColor':'#FFF'
			},
			'bottomMask':{
				'bottom':'0',
				'height':'50px',
				'backgroundColor':'#FFF'
			}
		},
		'noChina':{
			'topMask':{
				'top':'0px',
				'height':'50px',
				'backgroundColor':'#FFF'
			},
			'bottomMask':{
				'bottom':'20px',
				'height':'50px',
				'backgroundColor':'#FFF'
			}
		}
	},
	'taobao.com':{
		'status':0,
		'china':{
			'topMask':{
				'top':'20px',
				'height':'50px',
				'backgroundColor':'#FFF'
			},
			'bottomMask':{
				'bottom':'20px',
				'height':'50px',
				'backgroundColor':'#FFF'
			}
		},
		'noChina':{
			'topMask':{
				'top':'0px',
				'height':'50px',
				'backgroundColor':'#FFF'
			},
			'bottomMask':{
				'bottom':'20px',
				'height':'50px',
				'backgroundColor':'#FFF'
			}
		}
	}
}
```


## 业务流程

1. 获取当前内嵌页面的 地址url (iframe 进来的电商 url) ，得到当前url 的实体域名 (例如：taobao.com，tmall.com，jd.com)

1. 客户访问页面 -> 获取用户ip 
2. 查询用户是否属于中国
3. 如果是中国ip 直接 查询 实体域名下面的 `china` 遮罩层参数
4. 如果非中国ip 查询 实体域名下面 `status` 参数的值 ，如果为 0 查询 实体域名下面的 `noChina` 遮罩层参数 ,否则取 `china` 遮罩层参数


```
MATCH 1
1.	`dangdang.com`
MATCH 2
1.	`taobao.com`
MATCH 3
1.	`jd.com`
MATCH 4
1.	`tmall.com`
```

## demo 演示

https://github.com/panli-com/app-h5/tree/gh-pages/20151214

## 最后说明

由于遮罩层的样式和位置 都是由后台添加修改生成而来，所以辛苦添加数据的同学啦！！(*^__^*) 嘻嘻……