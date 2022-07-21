---
title: 本地写 Hexo Markdown 发到 GitPress 和自己的 blog
date: 2022-07-21 11:05:06
tags:
---

1. 解决 Hexo 不渲染 Markdown 的图片标签的问题：

安装插件：
```
npm install hexo-render-marked
```
如果有报错，可以再运行一下 npm audit。

config文件作如下修改：
```yml
post_asset_folder: true
#hexo-render-marked config:
marked:
  prependRoot: true
  postAsset: true
```

将图片放在文章同名文件夹，就可以渲染图像标签如：

```markdown
![](img.jpg)
![](articalname/img.jpg)
```

至此解决了渲染图片标签的问题，于是把 '\_posts' 文件夹创建为 GitHub Repo 并同步到 GitPress 中，这里按照 GitPress 的说明来进行就好，不做记录了。

2. 解决 GitPress 图片地址出错的问题

GitPress 中读取到图片标签会加上自己的域名，但没有经过 Hexo 自身渲染图片地址，于是和 deploy 到 blog 上的图片地址有冲突。
解决方法简单粗暴的把 Hexo 自身渲染的年月日标记去掉就好：
```yml
#permalink: :year/:month/:day/:title/
permalink: :title/
```

3. 发布文章的方法：

3\.1\. Hexo 发布到 blog：
本地创建新文章：
```
hexo new articalname
```
通过 Obsidian 编辑文章。
用 deploy 命令发布到自己的 blog。

3\.2\. git 命令发布到 GitPress：
在本地通过 git 命令把 '\_post' 文件夹同步到 GitHub。
GitPress 自动读取该 Repo 并发布。