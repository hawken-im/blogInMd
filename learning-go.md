---
title: 学 go 语言的一些小笔记
date: 2022-01-22 11:48:32
tags:
---

### Thu-Feb-3 2022 终于弄好了包管理 YearProgress 2022 这个项目暂时告一段落
在度假，网不好，因此没法翻墙，断断续续 baidu 了好几天，被弄到 CSDN 里兜兜转转了好几天！鬼打墙一样。
今天好不容易找了个咖啡店，翻出去了，立刻！马上！看到了这句话：
>"In the most basic terms, A package is nothing but a directory inside your Go workspace containing one or more Go source files, or other Go packages." 
划重点是"is nothing but" 

这个太关键了
中文文章要么就是高深莫测，搞得小白不知道他们是不是在故弄玄虚，要么就觉得包管理是不是太习以为常就干脆跳过。
这篇文章就叫深入浅出。即便是可能会很高深，但是文章也说了， "In the most basic terms"。 对，可以很难，但是本小白要的就是"most basic terms"。 文章链接在此： [https://www.callicoder.com/golang-packages/](https://www.callicoder.com/golang-packages/)

### Mon-Jan-24 2022
继续学了 flag 和 arguement，这样就可以在命令行输入酷酷的命令了。
go 的两个包分别是：
```
"flag"
"os"
```

### Sun-Jan-23 2022
昨天跑通了 json 的解析，今天开始系统的学习 struct 以及指针，这样就能在函数中读取 struct 并返回一整个 struct
今天主要看的书是 Head First Go
下一步应该要把包管理学了，不然现在所有的代码都是堆在一个文件里面
学完小半本 Head First Go 之前应该暂时不会更新 Year Progress 2022 代码了

### Sat-Jan-22 2022
今天学 go 语言解析 json，这两个教程解答了我很多问题：
https://eager.io/blog/go-and-json/
https://golangbyexample.com/struct-json-golang/
