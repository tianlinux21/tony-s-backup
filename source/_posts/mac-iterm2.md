---
title: Mac 配置终端iTerm2 + oh-my-zsh
tags:
- iTerm2 
categories:
- Mac配置
---

![](http://og20v8qdj.bkt.clouddn.com/iterm2.jpg)
iTerm2是Mac上的一款很强大的终端工具，其与oh-my-zsh搭配使得终端可以高度自定义。上图为oh-my-zsh的agnoster主题， 个人比较喜欢故而一直在使用。本文将从头开始一步步搭建属于自己的终端。
<!--more-->
## 安装
首先，我们进入iTerm2的官网下载相关版本[跳转链接](http://www.iterm2.com/downloads.html)，建议下载3.0.15稳定版。起初下载了最新版本3.1.x，发现新版的hotkey window相关功能发生了很大变化，不是很喜欢所以又换回了3.0版本。@.@
### 安装oh-my-zsh
安装完成之后，我们进入命令行将当前的shell改成zsh，之后使用curl下载oh-my-zsh.
```code
$ chsh -s /bin/zsh
$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
安装完成之后会默认使用robbyrussell主题。我个人比较喜欢agnoster字体，所以在终端输入
```code
$ vi ~/.zshrc
```
找到ZSH_THEME = "robbyrussell" 将其注释，另起一行重新输入ZSH_THEME = "angoster"或者直接将robbyrussell改成angoster也可以(本人更喜欢注释，哈哈)。
![快捷窗口设置](http://og20v8qdj.bkt.clouddn.com/hotkey.png)
本以为这样就可以了，结果重启终端后发现出现了乱码。我还是too naive了…根据git上相关提示，发现还需要安装字体才能正常显示出我们想要的效果来。
### 安装powerline fonts
接下来我们安装相关字体，命令如下所示。
```code
# clone
git clone https://github.com/powerline/fonts.git
# install
cd fonts
./install.sh
# clean-up a bit
cd ..
rm -rf fonts
```
至此，相关安装流程结束👏，接下来我们进行iTerm2相关的配置流程。附上agnoster配置完成后的终端图
![](http://og20v8qdj.bkt.clouddn.com/agnoster.png)

## iTerm2 配置
### 修改字体
首先我们选择iTerm2--Preferences--Profiles--Text 之后找到并点击Change Font，选择一个Powerline相关的字体即可。选好之后重启终端即可完成agnoster的配置。
![](http://og20v8qdj.bkt.clouddn.com/iTerm-config.png)
agnoster相关的配置这样就算完成了。不过还没有结束！iTerm2最最最好用的hotkey window还是得稍微说一下的！！
### hotkey window
如果您已经关闭了配置界面，直接安快捷键⌘ + , 进入配置页面。之后选择Keys，勾选hotkey下面的选择框并设置快捷键。如下图所示
![](http://og20v8qdj.bkt.clouddn.com/hotkey.png)
!!! iTerm2 3.1.x 版本虽然热键功能依旧存在，但是没了快捷窗口。本人有点难以理解这一改变(也有可能是我自己不会设置T.T)
勾选之后按一下快捷键，窗口就会出现了. 您还可以根据的喜欢去调整相关的透明度等、另外还可以在Profiles的window下给终端配置背景图片等等..总之，iTerm2功能非常强大，只要愿意配置，各种炫酷各种(｡･∀･)ﾉﾞ嗨~~

## 总结
第一次写不知道该如何写的更加言简意赅，若您发现有不足之处还请赐教。非常感谢