---
title: 数字添加千分符
tags:
- JavaScript
categories:
- 前端积累
---

&#8194;&#8194;近期工作碰到了数字加千分符的需求，其实是个很简单的需求不过由于本人开始用的方法出现了个bug所以后来搜了一下，结合自己写的正则一共发现了大约三种实现方法。
<!-- more -->
第一种方法最为简单也比较意外，第一次知道原来toLocaleString还可以这么用。代码如下：
```JavaScript
var num = 12332132;
num.toLocaleString('en-US');     // 12,332,132
```
toLocaleString() 方法返回这个数字在特定语言环境下的表示字符串。语法如下：
> numObj.toLocaleString([locales [, options]])

* locales: 可选. 缩写语言代码(BCP 47 language tag, 例如:cmn-Hans-CN)的字符串或者这些字符串组成的数组.
* options: 可选. 包含一些属性类，具体可根据需求设置。

这个方法用处很多，Object/String/Array/Date/Number 均可使用此方法。最为常见的用途在Date的使用上。如： new Date().toLocaleString()。

第二种方法是使用正则，我觉得是三种方法中比较好的一个。
```JavaScript
var result;
if(num>1000){
     var reg=/(\d{1,3})(?=(\d{3})+(?:$|\D))/g; //转化千分符
     num = num+"";
     result = num.replace(reg,"$1,");
}
```
* (?=pattern) 非获取匹配，正向肯定预查，在任何匹配pattern的字符串开始处匹配查找字符串，该匹配不需要获取供以后使用
* (?:pattern) 非获取匹配，匹配pattern但不获取匹配结果，不进行存储供以后使用。

第三种方法是本人之前写的，之前出现的诸如'123'会匹配成',123'的问题，后来经过修改之后也可以使用，不过相对于上面两种方法则较为麻烦，需要先将字符串翻转，之后匹配成功后在进行一次相同的操作。。。
```JavaScript
var input = 123321
var reverseStr = (input+'').split('').reverse().join('');
reverseStr = reverseStr.replace(/(\d{3})(?=[^$])/g, '$1,');
return reverseStr.split('').reverse().join('');
```
通过添加(?=[^$])使得此方法也可达到相同的效果，结合上面pattern模式使用[^$]来匹配非终止的三位数字达到目的。

嗯，完结~
