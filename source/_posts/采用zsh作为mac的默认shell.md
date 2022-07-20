---
title: 采用zsh作为mac的默认shell
tags: []
excerpt: ''
date: 2019-11-24 01:14:00
---

mac升级Catalina后，默认的shell是zsh，以前是bash  
本人本来就是新手小白，就算用了很久的bash，每次命令行输入都要上网查一下  
这次将就mac，换成了据说很厉害的zsh  
笔记如下：  
先查看一下电脑上都有些什么shell：  
cat /etc/shells  
再看看当前再运行什么shell：  
echo $SHELL  
确实还在用bash  
改成zsh：  
chsh -s /bin/zsh  
完毕