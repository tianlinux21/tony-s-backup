---
title: 解决通过nginx访问单页面应用出现net::ERR_CONTENT_LENGTH_MISMATCH的问题
tags:
- nginx
categories:
- 前端积累
---

今天遇到一个问题，新项目启动之后在console出现只有一行net::ERR_CONTENT_LENGTH_MISMATCH的报错，没有其他信息；项目使用nginx做了反向代理，所以查看了一下nginx的错误日志(MacOS下nginx日志位置 /usr/local/var/log/nginx/error.log)，发现错误如下：
```code
2018/03/12 11:36:52 [crit] 26908#0: *82084 open() "/usr/local/var/run/nginx/proxy_temp/8/02/0000000028" failed (13: Permission denied) while reading upstream, client: 192.168.24.112, server: 192.168.24.112, request: "GET /dev/app.js HTTP/1.1", upstream: "http://127.0.0.1:8031/app.js", host: "192.168.24.112:8083", referrer: "http://192.168.24.112:8083/dev/"
```

如错误日志所示，没有proxy_temp读写权限所导致的问题；后来查了一下，因为nginx会缓存大文件到proxy_temp目录中所以没有读写权限就会出现该错误。
对应的解决方法：
* 使用chmod去将proxy_temp的权限改为rwx
* 使用chown去修改目录的owner为root，之后使用管理员权限运行nginx(sudo nginx)
