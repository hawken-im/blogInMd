---
title: 搭建FTP服务器
tags: []
excerpt: ''
date: 2019-11-26 00:32:00
---

详细过程有点懒得写，链接一个教程  
[https://www.howtoforge.com/tutorial/ubuntu-vsftpd/](https://www.howtoforge.com/tutorial/ubuntu-vsftpd/)  
这里踩到第一个坑是被动模式  
因为有防火墙，一定要被动模式才能连通  
被动模式是这么一回事  
[![](https://4.bp.blogspot.com/-0FCUXqtqBMc/XdwBf5cmwTI/AAAAAAAAGBM/xphTGV2Z4SoLMUbuJeKqZNIyKtZQPvJMQCK4BGAYYCw/s320/221601380466453.jpg)](http://4.bp.blogspot.com/-0FCUXqtqBMc/XdwBf5cmwTI/AAAAAAAAGBM/xphTGV2Z4SoLMUbuJeKqZNIyKtZQPvJMQCK4BGAYYCw/s1600/221601380466453.jpg)  
  
开启被动模式在filezilla的log中会看到：  
p.p1 {margin: 0.0px 0.0px 0.0px 0.0px; font: 11.0px 'Helvetica Neue'; color: #008000; background-color: #ffffff} span.Apple-tab-span {white-space:pre}  

Response: 227 Entering Passive Mode (H1,H2,H3,H4,P1,P2).

这里的P1\*256+P2，就是当前被动模式的随机端口号  
  
防火墙中开启设定好的端口范围，再重启一下vsftp服务  
搞定了