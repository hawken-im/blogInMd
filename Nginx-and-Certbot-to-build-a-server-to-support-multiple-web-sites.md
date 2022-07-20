---
title: Nginx and Certbot to build a server to support multiple web sites
date: 2021-08-01 16:57:00
tags:
---
### Install and config nginx first.
I followed these two instructions:
[](https://phoenixnap.com/kb/how-to-install-nginx-on-ubuntu-20-04)
[](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04)

Remember to config "sites-available" seperately, try not to config the global config file, for two reasons:
1. It'll be easier to maintain.
2. Certbot is not that clever, so we want to leave the global config file to Certbot.

### Read Certbot manual first then follow quick instructions from Certbot homepage
Follow the official instructions to install Certbot correctly.
[](https://certbot.eff.org/instructions)
Then we need to choose a command to call a plugin to get CA.
After I finished reading, I found out many unofficial instructions online are outdated. 
[](https://certbot.eff.org/docs/using.html#nginx)
If we install Certbot correctly, we only need to use command:
```
certbot --nginx
```
Then Certbot can do all for you. Even can create a cron job to renew certificate automatically.