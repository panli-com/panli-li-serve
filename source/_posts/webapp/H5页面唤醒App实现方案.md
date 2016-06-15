title: H5页面唤醒App实现方案
date: 2016-06-14 10:18:19
tags:
  - app
  - mobile
  - webapp
  - javascript
  - h5
categories:
  - mobile
---

## 需求说明

H5 分享页 在 微信 `WebView` 下载按钮点击后，打开 `AppStore `下载页面；
如果是浏览器打开，则判断是否装了`APP`，如果装了则打开拼邮界面。

## 『经浏览器唤起APP』的最佳实现方案是怎样的？

下面 一一作出解决方案

### 遇到的主要问题

无法判断用户是否安装APP，来采用何种跳转逻辑：

1. `iOS` 有原生的 `Smart Banner`，可以帮助判断是否安装 `APP` 并跳转，
但也仅限于 `safari` 浏览器，并且不可定制样式和跳转URL。
需要通过 `schema` 来唤起 `APP`，因为需要带上具体的页面参数。

2. 在比较旧的` iOS `版本里，业界有一个比较通用的办法，是可以通过 `iFrame `尝试唤起 `APP`，
以一个时间差来判断用户手机里是否已安装，再来决定是否跳到 `appStore`。
然而最新的 `iOS `中，这一套方案已经失效，`iFrame` 不再有效果。

3. 尝试过用 `setTimeout` 来首先直接唤起APP，然后再唤起 `appStore`。
这样的话，如果没有安装APP，会有一个难看的提示『该网址已经失效』，还需要手动X掉。
尝试通过 `setTimeout ` 来首先直接唤起 `APP` ，然后再跳转到另一个页面再唤起 ` appStore `。

这样的话新页面虽然可以将『该网址已经失效』给顶掉，
但是同时也会把正常唤起APP的提示『是否打开APP』也给顶掉。

4. 如果用户是通过微信、qq等内置webview启动这一操作，那么提示用户启用 `safari` 打开并再走一次以上逻辑。
有的APP可以直接通过微信qq判断并唤起，
比如知乎？不知道此中是有友好协议，还是我并没有完全搞清楚原理，需要大家解答一下。

### 简单调查

简单调查了一下某些其他应用，发现大家并没有一套通用并完美的方案：

1. 『知乎』及『网易云音乐』提供了两个入口，一个供跳转到APP，一个供跳转到 `appStore`。
未安装点击跳转到APP会有错误提示。

2. 腾讯视频只有一个按钮，貌似是第一次点它会给你跳到 `appStore` ，此后再点它就会给你唤起APP。
未安装点击会有错误提示。

3. 简书则是直接唤起APP。未安装点击会有错误提示。

大体上就是这三类方案，可是始终没有一个满足最上面需求的完美方案。

### 实现方案

1. 微信客户端与qq浏览器客户端

    ```
    跳转到下载地址

    至于为什么？
    有些app会阉割掉深链接的功能，例如微信，QQ。
    这时候就需要引导用户通过打开外部浏览器来实现深链接的功能
    ```
2. ios9 Safari 

    ```
    直接打开 `Panli APP` 的 移动深链接, 如果安装了 直接弹出是否打开 `Panli APP`, 
    如果未安装，Safari 会弹出『该网址已经失效』，然后跳转到 `appStore`
    ```

### demo

- [打开地址 https://ipanli.github.io](https://ipanli.github.io/webapp/20160612/)

- 二维码扫一扫

  ![demo](/update/20160614/demo.png)


## android

经过小规模的测试，得到以下结论

由于下载走的是 腾讯应用宝 , 在安卓的微信下面，需要借助 腾讯应用宝来打开App 的,
意思就是说，当安卓客户端未安装 应用宝的时候 ,中转页面会有一个 `普通下载` 和 `腾讯应用宝安全打开` 2 个选项 
- 普通下载 ,不明显，且点击会有安全提示!
- 腾讯应用宝安全打开 会先下载应用宝 （家族产品的霸道，有种你别用微信，人在屋檐下呀,囧！）

当然如果你安装了 应用宝 和 Panli APP 的是 是直接打开APP 的，
（部分安卓机有Bug 或者权限问题 ，尤其是 谷歌自家的，这个无能为力，因为走的是 应用宝，不是我们能控制的）



## 主要代码实现

```js
if(isWeixinBrowser() || isQQBrowser()){
            window.open(downUrl)
            PL.open({
                content: '正在为您跳转...',
                time: 5
            });
        }else{
            if(isAndroid){
                //android
                //唤醒app并阻止接下来的js执行
                $('body').append("<iframe src='panliapp://openapp' style='display:none' target='' ></iframe>");

                //没有安装应用会跳转下载地址
                setTimeout(function(){window.location = Android},600);
            }else{
                //ios
                //唤醒app
                window.open('panliapp://openapp', "_self");

                //没有安装应用会跳到 appStore
                setTimeout(function(){window.location = 'itms-apps://itunes.apple.com/app/id590216292'},300);
            }
}
```
