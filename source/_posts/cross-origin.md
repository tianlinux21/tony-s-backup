---
title: 使用postMessage解决iframe跨域问题
tags:
- JavaScript
categories:
- 前端积累
---

&#8194;&#8194;我们在使用iframe的时候常常会有子frame内部的页面控制父级页面退出登录或者一些其他的功能需求，但是常常会碰到这样的错误提示
```JavaScript
Uncaught DOMException: Blocked a frame with origin "http://www.xxxx.com" from accessing a cross-origin frame.
```
如上所示，之前试过使用网上所说的window.top.location.href来直接修改外部链接结果失败了。今天碰巧看到了postMessage，发现可以用来解决这个问题。
<!-- more -->
> window.postMessage() 方法可以安全地实现跨源通信。通常，对于两个不同页面的脚本，只有当执行它们的页面位于具有相同的协议（通常为https），端口号（443为https的默认值），以及主机  (两个页面的模数 Document.domain设置为相同的值) 时，这两个脚本才能相互通信。window.postMessage() 方法提供了一种受控机制来规避此限制，只要正确的使用，这种方法就很安全。——引自MDN

```JavaScript
// 子页面(此处只考虑一层iframe的情况，如果嵌套多层，则使用window.top指向最外层)
window.top.postMessage('xxx', '*');

// 父页面, top
window.addEventListener('message', function(e) {
    console.log(e.data);    // e.data->'xxx' 即子页面通过postMessage传递过来的值
}, false);
```
**在iframe中只需上述代码即可完成跨域问题，关键是对于iframe/frames可以兼容至IE8！其他场景下使用postMessage时IE兼容性较差，可以说是完全不支持的，所以使用时需要根据实际情况。**

下面是postMessage的语法
> otherWindow.postMessage(message, targetOrigin, [transfer]);

#### otherWindow
&#8194;&#8194;其他窗口的一个引用，比如iframe的contentWindow属性、执行window.open返回的窗口对象、或者是命名过或数值索引的window.frames。
#### message
&#8194;&#8194;将要发送到其他 window的数据。它将会被结构化克隆算法序列化。这意味着你可以不受什么限制的将数据对象安全的传送给目标窗口而无需自己序列化
#### targetOrigin
&#8194;&#8194;通过窗口的origin属性来指定哪些窗口能接收到消息事件，其值可以是字符串"\*"（表示无限制）或者一个URI。在发送消息的时候，如果目标窗口的协议、主机地址或端口这三者的任意一项不匹配targetOrigin提供的值，那么消息就不会被发送；只有三者完全匹配，消息才会被发送。这个机制用来控制消息可以发送到哪些窗口；如果你明确的知道消息应该发送到哪个窗口，那么请始终提供一个有确切值的targetOrigin，而不是*。*不提供确切的目标将导致数据泄露到任何对数据感兴趣的恶意站点*
