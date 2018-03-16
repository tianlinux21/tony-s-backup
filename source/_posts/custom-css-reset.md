---
title: 常用的input默认样式重置
tags:
- css
categories:
- 前端积累
---
> 积累一些常用的去除input浏览器自带的默认样式，select以及其他属性修改默认样式尚在探索中。尤其是select样式= =感觉好像只能模拟select标签，无法直接美化其样式

<!-- more -->

```css
/* 去除上下小箭头 */
input[type="number"] {
    -moz-appearance: textfield;
}
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
    /*visibility: hidden;*/
    -webkit-appearance: none;
	margin: 0;
}

/* 搜索去除默认样式 */
input[type="search"] {
	-webkit-appearance: none;
}

input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-decoration {
	-webkit-appearance: none;
}

/* 记住密码去除黄色背景 */
/* 方法一&二同时使用效果更佳，只使用一个会有兼容性问题 */
input::-webkit-autofill {
    /* method 1 */
    transition: background-color 50000s ease-in-out 0s;    /* 去掉黄色背景 */
    /* method 2 */
    box-shadow: 0 0 0 1000px white inset;    /* 覆盖黄色背景 */
    -webkit-text-fill-color: #3a3a3a;    /* 希望的输入框颜色 */
}

/* 去除密码框输入后的小眼睛 */
input[type="password"]::-ms-reveal {
    visibility: hidden;
}

```
