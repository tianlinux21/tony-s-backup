---
title: border double 快速实现三横线按钮
tags:
- css
categories:
- 前端积累
---

在慕课网看了张鑫旭大神的css深入理解之border，关于border:double的用法非常赞。很简单的几行代码就实现了常用的点击显示菜单的按钮，而且无兼容性方面的问题！因此记录一下，

<!-- more -->

参考以下代码:
``` css
html, body, div{
    margin: 0;
    padding: 0;
}
.demo {
    height: 20px;
    width: 120px;
    border-top: 60px double;
    border-bottom: 20px solid;
}

```

``` html
<div class="demo"></div>
```
double属性两条线之间的间隙距离 = 上下等高，间隙在上下高度的基础上 +/- 1 (如：7px = 2px + 3px + 2px)

不过这种方法有时不太容易控制线线之间的空隙以及线的长度，利用伪元素:before :after也可以实现相同的效果，在不需要兼容IE的情况下，使用伪元素实现也是一个好的选择，代码量会稍多一点。
