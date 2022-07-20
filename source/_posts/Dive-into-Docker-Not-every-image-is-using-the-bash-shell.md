---
title: Dive into Docker - Not every image is using the bash shell
tags: []
excerpt: ''
date: 2021-05-18 16:06:00
---

Try to get into the shawdowsocks container created by docker.

Found this command:

 docker exec -it <container> bash

It didn't work. And I found this:

https://mkyong.com/docker/docker-exec-bash-executable-file-not-found-in-path/

  

Noticed not every image is using the bash shell.

Then tried this:

 docker exec -it <container> sh

It actually worked.