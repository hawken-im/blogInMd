---
title: 从零开始在 Ubuntu 20.04 上Build Quorum 并用本地 Rum App 进行连接
date: 2022-01-15 00:47:28
tags:
---

### 2022 Feb 13版本更新：
新版 quorum 里 jwt token 是可选项，如果留空的话系统会自动生成一个。

---

Rum App 发布后我搭建了一个 windows server 运行，但一直感觉不够炫酷，于是折腾了一台 Ubuntu 主机。在主机上自己 Build Quorum，并运行，并在两位大佬轮番指导下才通过本地 Rum App 连接成功。两位大佬一位是 samson 一位是 wanming，这篇文章圈不出来他们本人。但是真的很感谢他们的热心帮助。如果大佬看到希望可以在评论区留言认领我的感谢。

正文开始

##  1. 从零开始的第一步 - 在服务器上获取 Rum System

这一步我们会通过 git 命令从 github 上直接克隆一个 Rum System 到我们的服务器上。
所以你需要先在服务器上安装 git：
```
sudo apt-get install git
```

安装完成输入命令：
```
git --version
```

检查一下是否安装成功。
接下来就是从 github 上通过 git clone 命令来克隆 Rum System。
Rum System 在 github 上的地址是：
https://github.com/rumsystem/quorum

点击“Code”按钮会出现下拉菜单，菜单中选择“SSH”这一栏，就会出现仓库地址了。
{% asset_img ScreenShot.png %}

将仓库地址放到克隆命令后，回车执行命令行：
```
git clone git@github.com:rumsystem/quorum.git
```

如果发现系统提示我们无法连接，是因为 git clone 命令是通过 SSH 进行连接的，我们需要在自己的 github 账号里加入我们的 SSH 公钥。

步骤可以参考 github 的官方教程，链接如下：
https://docs.github.com/en/authentication/connecting-to-github-with-ssh

克隆完成后可以“ls”一下看看是不是有了“quorum”这个文件夹。

## 2. Build

现在可以进入文件夹去 build 我们的 Rum System。
```
cd quorum
```

在根目录里执行开发人员准备好的脚本文件就好：
```
./scripts/build.sh
```

这个时候有可能会报错，是说我们还没有安装 go 语言。那我们就安装一下好了。
go 语言的官方下载页面在这里：
https://go.dev/dl/

进去后下载 linux 的版本就好：
{% asset_img go.png %}

你可以通过 scp 命令上传到服务器，也可以在服务器上用 curl 命令把这个文件下载下来。
我这里是在本地用的 scp 命令：
```
scp [本地tar.gz] [用户]@[服务器地址]:[服务器文件路径]
```

上传成功后，到文件所在位置输入如下命令：
```
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.17.6.linux-amd64.tar.gz
```

然后把 go/bin 输入到环境变量中，只需要把下面的语句放到 /etc/profile 文件内：
```
export PATH=$PATH:/usr/local/go/bin
```

确认一下是否安装成功：
```
go version
```

go 语言的官方安装教程在这里：
https://go.dev/doc/install

再次 Build 成功，进入下一步。

## 3. 在服务器上运行 Quorum

Build 成功的可执行文件存在 dist 文件夹中。cd 进 dist 去，ls 看到 dist 里面的文件夹里有个 linux 文件夹，再次 cd 进去，就到了 linux 系统的可执行文件的所在地了。

{% asset_img dist.png %}

直接 ./quorum 运行是不行的，需要加一些参数，我的带参数的运行命令是这样的：
```
RUM_KSPASSWD=[我的密码] ./quorum -peername [我的节点名] -listen /ip4/0.0.0.0/tcp/7000  -apilisten 0.0.0.0:8002 -peer /ip4/94.23.17.189/tcp/10666/p2p/16Uiu2HAmGTcDnhj3KVQUwVx8SGLyKBXQwfAxNayJdEwfsnUYKK4u -peer /ip4/132.145.109.63/tcp/10666/p2p/16Uiu2HAmTovb8kAJiYK8saskzz7cRQhb45NRK5AsbtdmYsLfD3RM -ips [服务器的公网IP] -ips 127.0.0.1
```

这样就能运行成功了。
运行成功的界面应该长这样：
{% asset_img successed.png %}

会跳出一些 warning 什么的，可以暂时忽略掉。

这个时候可以输入一个 curl 命令检查一下是否连接成功：
```
curl -k https://127.0.0.1:8002/api/v1/groups
```

成功的话会返回一个当前种子网络的状态的消息。

进入下一步之前再保存一个密钥，它位于 quorum 文件所在的文件夹里，cd 进 cert 文件夹，里面有两个文件分别是 server.key 和 server.crt。输入命令：
```
cat server.crt
```

把返回的密钥复制保存在本地。

新版本里 jwt token 不是必须的，这里也可以去存一个备用，jwt 位于 quorum 运行根目录所在的 config 文件夹里，里面有个后缀为 .toml 的文件，cat 或 vi 打开就能找到 jwt。

## 4. 本地 Rum APP 连接服务器

这下万事俱备了，我们在本地打开 Rum APP，从菜单项“节点与网络”中选中“外部节点”。
{% asset_img outterpeer.png %}

到了填入节点信息的步骤，把我们在上一步收集到的 jwt 和 server.crt 填进去就好了：
{% asset_img peerinfo.png %}

顺利的话，应该可以看到“外部节点模式”亮绿灯了：
{% asset_img green.png %}

不顺利的话，比如我，踩到的坑我在下一个小节总结一下，看看读者能不能顺利回避：

## 踩到的坑：

1. 如果是新手小白的话可能会在各种文件夹和目录之间反复横跳找不到方向。这个看仔细一点就好了。
2. 防火墙可能会阻止本地 APP 连接服务器。解决办法是打开端口 433，7000，8002。
3. 最坑我的是我的云主机买的内存太小，如果内存溢出 quorum 进程马上就会被杀死。这个问题我一直无法定位，走了好多弯路，最后是求助大佬帮我发现的。解决办法是加了 1G swap。
4. 最后是一个很好用的工具 tmux，可以帮我们保持住 quorum 的运行的同时开启别的命令行界面进行测试。