---
title: 在ubuntu上安装python3.8.2
tags: []
excerpt: ''
date: 2020-03-10 17:32:00
---

强迫症患者发现远程服务器的python版本不够update。 最新的python版本是3.8.2。   
找到一个教程：  
[https://tecadmin.net/install-python-3-8-ubuntu/](https://tecadmin.net/install-python-3-8-ubuntu/)  
  
安装以下包，用于compile最新的python。  
 sudo apt-get install build-essential checkinstall  
sudo apt-get install libreadline-gplv2-dev libncursesw5-dev libssl-dev \\ libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev  
  
然后去下载python 3.8.2，并解压  
cd /opt  
sudo wget https://www.python.org/ftp/python/3.8.2/Python-3.8.2.tgz  
sudo tar xzf Python-3.8.2.tgz  
  
make 并安装  
 cd Python-3.8.2  
sudo ./configure --enable-optimizations sudo make altinstall  
  
检查版本：  
 python3.8 -V Python-3.8.2  
  
删除掉安装包：  
cd /opt sudo rm -f Python-3.8.2.tgz