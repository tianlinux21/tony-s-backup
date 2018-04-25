---
title: LC_CTYPE cannot change locale (UTF-8)错误解决方法
tags:
- ssh
categories:
- Mac配置
---

&#8194;&#8194;因本人在GitHub提交代码时会在终端显示如下的警告提示：
```code
warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory
```
故记录一下。
原因：此警告信息发送的原因是 OpenSSH 服务器和 OS X ssh 终端客户之间的问题。
过程：local ssh client is sending your LC_* environment variables to remote sshd server. In other words, SSH will try to set every LC_* variable you have set on your local OSX system on the remove server too.——摘自stackoverflow

解决方法很简单，这里介绍一个修改ssh_config的方法，之前修改iTerm中的locale值发现不具有通用性，所以最终选择了修改ssh_config;如下：

```code
$ sudo vi /etc/ssh/ssh_config
# remove or comment out as follows:
#SendEnv LANG LC_*

```

or, 远程服务器安装需要的字符集
```code
# localedef -i en_US -f UTF-8 en_US.UTF-8
```
