---
title: 给服务器开通BBR
tags: []
excerpt: ''
date: 2019-12-14 19:13:00
---

Google developed a TCP Congestion Control Algorithm (CCA) called TCP Bottleneck Bandwidth and RRT (BBR) that overcomes many of the issues found in both Reno and CUBIC (the default CCAs). This new algorithm not only achieves significant bandwidth improvements, but also lower latency. TCP BBR is already employed with google.com servers, and now you can make it happen--so long as your Linux machine is running kernel 4.9 or newer.