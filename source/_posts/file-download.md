---
title: js实现文件下载
tags:
- JavaScript
categories:
- 前端积累
---

文件下载是日常开发中常见的需求，当我们从服务器获取到URL地址的时候便需要使用js来实现下载的功能，而只将a标签href的值设为需要下载的文件地址对于图片是不适用的。此时，可以HTML5中对a标签添加了download属性，为我们下载文件与图片提供了很大的帮助。
> 遗憾的是，只有Firefox与chrome支持download属性

<!-- more -->

``` javascript
    let url = 'xxxx';   // ajax 请求到的文件链接地址
    let a = document.createElement('a');
    a.setAttribute('href', url + name);
    a.setAttribute('download', '');
    let evObj = document.createEvent('MouseEvents');
    evObj.initEvent('click', true, true);
    a.dispatchEvent(evObj);
```
这其中使用了createEvent()方法创建了新的Event对象，createEvent对象语法如下:
> createEvent(eventType)

| 参数            | 描述                          |
| -------------  |:-------------------- --------:|
| eventType      | 想获取的 Event 对象的事件模块名。 |

该方法将创建一种新的事件类型，该类型由参数 eventType 指定。注意，该参数的值不是要创建的事件接口的名称，而是定义那个接口的 DOM 模块的名称。
具体参数可以查看[w3School](http://www.w3school.com.cn/xmldom/met_document_createevent.asp)
关于自定义Event对象，有很多相关的文章，感兴趣的可以自行搜索哦
