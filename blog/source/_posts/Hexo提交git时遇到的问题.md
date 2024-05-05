---
title: Hexo提交git时遇到的问题
top: false
cover: false
toc: true
mathjax: false
date: 2024-05-02 17:25:32
author:
img:
coverImg:
password:
summary:
tags: HEXO
categories: [HEXO建站指南]
---
# Hexo 提交git时遇到错误

在`hexo d`阶段时遇到如下错误

>fatal: unable to access 'https://github.com/Junb0Dong/Junb0Dong.github.io.git/': Failed to connect to github.com port 443 after 21107 ms: Couldn't connect to se rver FATAL Something's wrong. Maybe you can find the solution here: https://hexo.io/d ocs/troubleshooting.html Error: Spawn failed at ChildProcess.<anonymous> (C:\Users\20200\Desktop\hexo\blog\node_modules\h exo-deployer-git\node_modules\hexo-util\lib\spawn.js:51:21) at ChildProcess.emit (node:events:518:28) at cp.emit (C:\Users\20200\Desktop\hexo\blog\node_modules\cross-spawn\lib\en oent.js:34:29) at ChildProcess._handle.onexit (node:internal/child_process:294:12)

分析错误，怀疑可能是网络链接问题。

但是我测试能科学上网，也能在网页上登录github并提交代码，但是在终端上就不可以提交，总是显示网络问题，这个困扰我两天，搞得懵懵的。

后来在网上看到了解决方案：

[Git报错： Failed to connect to github.com port 443 解决方案](https://blog.csdn.net/zpf1813763637/article/details/128340109)

[解决error: cannot overwrite multiple values with a single value Use a regexp, --add or --replac](https://blog.csdn.net/qq_35812205/article/details/135048261)

发现问题原来是主机上vpn的端口设置问题，于是在git bash上进行如下设置：

```bash
git config --global --unset-all http.proxy #取消全局所有代理
git config --global http.proxy http://your.proxy.server:port #重新设置代理
```

其中`http://your.proxy.server:port`为代理服务器地址和端口

**命令中的主机号（127.0.0.1）**是使用的代理的主机号(自己电脑有vpn那么本机可看做访问github的代理主机)，即填入127.0.0.1即可，否则填入代理主机 ip(就是网上找的那个ip)

**命令中的端口号（7890）**为代理软件vpn(代理软件不显示端口的话，就去Windows中的代理服务器设置中查看)或代理主机的监听IP，可以从代理服务器配置中获得，否则填入网上找的那个端口port 

最后，我在终端输入：

```bash
git config --global --unset-all http.proxy	#取消全局所有代理
git config --global http.proxy http://127.0.0.1:7890	#重新设置代理
```

