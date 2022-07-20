---
title: SSH创建密钥登陆远程服务器
tags: []
excerpt: ''
date: 2019-11-24 00:53:00
---

网上教程太多了，这里简单做个笔记好了：  
在本地terminal输入：  
ssh-keygen  
生成密钥对  
要不要给密钥加密，我选择的是加密  
输入了一个超长超难的密码，“就不告诉你密码系列”，图个开心  
然后把密钥上传到服务器就好  
上传方法是，本地terminal输入：  
ssh-copy-id user@host  
输入成功后可以到服务器上把ssh配置修改为不允许密码登陆  
方法是，登入服务器找到ssh配置文件，通常在/etc/ssh/ssh\_config  
在文件内找到  
\# PasswordAuthentication yes  
去掉注释后把yes改成no  
完毕