title: 服务器端世界时间(UTC)转换客户端时区时间
date: 2015-11-03 07:47:56
tags:
  - javascript
  - getTimezoneOffset
categories:
  - node
---

最近在做项目的时候，一直出现 客户端时间不对的问题,鉴于顺应 上个前端开发的布道，在设置时间方面，也一直按照以往的惯例.
由于时间是海外客户，在取服务器时间的接口上，总是比北京时间提早8小时，于是希望服务器接口返回的时间是格林威治时间，
根据客户端的时区转换时间。

> gg接口
>GetDateTimeUtc     返回UTC标准时间毫秒
>GetDateTimeStamp   返回标准UTC时间戳
##　服务接口返回格林威治时间

```
$.ajax({
    type: "POST",
    url: "/App_Services/wsDefault.asmx/GetDateTimeStamp",
    dataType: "json",
    contentType: "application/json;utf-8",
    timeout: 10000,
    error: function () { },
    success: function (msg) {
        if (msg)
            ajaxInit(parseFloat(msg.d));
    }
});
```


## 根据客户端的时区获取时差

```
function clientTimeZoneT() {
    //获得时区偏移量
    var timeOffset = new Date().getTimezoneOffset();
    //获得时区小时偏移基数
    var hour = parseInt(timeOffset / 60);
    //获得时区分钟偏移基数
    var munite = timeOffset % 60;
    var prefix = "-";
    if (hour < 0 || munite < 0) {
        prefix = "+";
        hour = -hour;
        if (munite < 0) {
            munite = -munite;
        }
    }
    hour += " ";
    munite += " ";
    if (hour.length == 2) {
        hour = "0" + hour;
    }
    if (munite.length == 2) {
        munite = "0" + munite;
    }
    var TimeZone = prefix + hour + munite;

    var TimeZoneJ = {
        TimeZone: TimeZone,
        Minute:timeOffset,
        millisecond: -(timeOffset*60*1000)
    }

    return TimeZoneJ;
}
```
clientTimeZoneT 函数 返回一个 json 对象
`TimeZone` 时区差
`Minute`   相差分钟数
`millisecond` 毫秒数 ：为了和服务器返回的时间做对应客户端时间


## JavaScript getTimezoneOffset() 方法

返回格林威治时间和本地时间之间的时差：

```
var d = new Date()
var n = d.getTimezoneOffset();
```

n 输出结果:

```
-480
```

## 定义和用法

getTimezoneOffset() 方法可返回格林威治时间和本地时间之间的时差，以分钟为单位。
例如，如果时区为 GMT+2, 将返回-120 。
注意： 由于使用夏令时的惯例，该方法的返回值不是一个常量。
提示： 协调世界时，又称世界统一时间，世界标准时间，国际协调时间，简称UTC（Universal Coordinated Time）。
注意： UTC 时间即是 GMT（格林尼治） 时间。

## 返回值

Number : 本地时间与 GMT 时间之间的时间差，以分钟为单位。

## 最终方案

选择了 GetDateTimeStamp   返回标准UTC时间戳

遇到的坑 是 `GetDateTimeStamp` 给我返回的是 10 位数的 时间戳 哈哈 ，所以需要给返回的值 * 1000

可以看到一下代码 返回的时间戳 * 1000 后在交给 js 处理。

```
$.ajax({
    type: "POST",
    url: "/App_Services/wsDefault.asmx/GetDateTimeStamp",
    dataType: "json",
    contentType: "application/json;utf-8",
    timeout: 10000,
    error: function () { },
    success: function (msg) {
        var millisecond = parseInt(clientTimeZoneT().millisecond);
        var HDateTime = parseFloat(msg.d * 1000);     
        if (msg)
            ajaxInit(HDateTime);
    }
});
```

---
