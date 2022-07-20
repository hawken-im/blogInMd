---
title: 把kindle的书全部下载到电脑上！
date: 2022-06-19 23:40:46
tags:
---

亚马逊宣布 Kindle 将退出中国市场。
买了的书咋个办？亚马逊给的说法是书仍然可以下载并在阅读器中阅读。
但是我的泡面盖子已经好多年历史了，Pad 上的 APP 又给人不踏实的感觉——想起之前还经历过 Pad 版本太旧，Kindle APP 不支持的情况。

所以趁自己在恐慌期间有动力，把下载 kindle 电子书的方法研究出来了：
（有拖延症的朋友也不必太着急，官宣是在2023年6月30日才正式停止运营。）

第一步，工具下载：
首先要感谢这位大佬，这个工具是他创始的，还要感谢之后涌来的一群程序员大佬，做出了图形化界面，才有我们小白的操作空间：
{% asset_img credit.png %}
下载地址在这里：
https://github.com/yihong0618/Kindle_download_helper/releases

如果某种不明原因打不开这个网站，可以公众号回复“kindle”获取下载链接。

{% asset_img guifiles.png %}
找到自己操作系统所对应的文件进行下载。
第一个是 linux，第二个是 macOS，第三个是 windows。

第二步，打开下载工具：
{% asset_img steps.png %}

第二.1步，点击登录（1 号红圈处），进入自己的 Kindle 图书管理页面：
{% asset_img f122.png %}

在这个页面按 F12 按键。以我对小白的了解（我就是），我认为有必要讲一下 F12 在哪里：
{% asset_img f12.jpg %}

第二.2步，在调试窗口中找两串神秘文本，粘贴到相应的位置：
出现了调试窗口，在这个窗口中搜索“csrf”，可以看到“csrfToken=""”这一串文本。
{% asset_img csrf.png %}

把双引号里面的文本复制下来，粘贴到下图 3 号圆圈处。注意不能复制双引号。
{% asset_img steps.png %}

回到调试窗口，找到“network”这一栏，随便找一个带有 200 这个数字的数据，打开：
{% asset_img network.png %}

在小窗口中找到“cookie”，鼠标右键，复制下来：
{% asset_img cookievalue.png %}

粘贴到下图 2 号圆圈出：
{% asset_img steps.png %}

第二.3步，点击 4 号圆圈处，获取下载列表，等一小会儿，就会出现自己的书了；
第二.4步，点击 5 号圆圈处“浏览”按钮，指定自己的书要下载到哪里（如果是苹果电脑，必须点一次浏览，这样才能给电脑授权）：
{% asset_img steps.png %}

第二.5步，点击 6 号圆圈处的下载全部按钮。
这个时候会出现进度条，和一些进度提示，耐心等待完成就好了。

第三步，转换成 epub 文件：
下载下来了后缀名是“.azw”的文件，用 Kindle APP 就可以打开了，但是我还是觉得 epub 文件更通用一点，这里提供一个转换工具：
https://www.neat-reader.cn/downloads/converter
{% asset_img neatconverter.png %}
