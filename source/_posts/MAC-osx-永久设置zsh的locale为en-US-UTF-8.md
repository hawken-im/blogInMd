---
title: MAC osx 永久设置zsh的locale为en-US.UTF-8
tags: []
excerpt: ''
date: 2021-01-15 10:28:00
---

 之前每次都要输入export locale=en-US.UTF-8

网上的教程也没有讲清楚zsh启动的配置文件到底在哪里。

我这次找到了。

在/etc/zshrc

在这个文件后面加入

export locale=en-US.UTF-8

就好了。

当然这个文件权限是readonly，要在vim前面加个sudo，这个也是教程没有提到的。