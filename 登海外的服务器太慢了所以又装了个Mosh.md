---
title: 登海外的服务器太慢了所以又装了个Mosh
tags: []
excerpt: ''
date: 2020-03-10 19:11:00
---

装mosh的时候遇到locale的坑，这里记录一下：  
提示跟locale相关的错误，可以同时在服务器端和本地输入locale 命令看一下自己的locale list是不是UTF-8一套的。  
如果不是就需要用export命令修改一下。  
我修改了本地locale 为en\_US.UTF-8，问题得到了解决。  
  
命令  
locale 查看当前locale  
  
export LANG=en\_US.UTF-8  
export LC\_ALL=en\_US.UTF-8  
之后就可以mosh了