---
title: 记录 postgre 的小坑一枚
date: 2022-07-24 01:34:49
tags:
---

Source:
https://serverfault.com/questions/110154/whats-the-default-superuser-username-password-for-postgres-after-a-new-install

**CAUTION** The answer about changing the UNIX password for "postgres" through "$ sudo passwd postgres" is not preferred, and can even be **DANGEROUS**!

This is why: By default, the UNIX account "postgres" is locked, which means it cannot be logged in using a password. If you use "sudo passwd postgres", the account is immediately unlocked. Worse, if you set the password to something weak, like "postgres", then you are exposed to a great security danger. For example, there are a number of bots out there trying the username/password combo "postgres/postgres" to log into your UNIX system.

What you should do is follow **Chris James**'s answer:

```
sudo -u postgres psql postgres

# \password postgres

Enter new password: 
```

To explain it a little bit. There are usually two default ways to login to PostgreSQL server:

1.  By running the "psql" command as a UNIX user (so-called IDENT/PEER authentication), e.g.: `sudo -u postgres psql`. Note that `sudo -u` does NOT unlock the UNIX user.
    
2.  by TCP/IP connection using PostgreSQL's own managed username/password (so-called TCP authentication) (i.e., **NOT** the UNIX password).
    

So you _never_ want to set the password for UNIX account "postgres". Leave it locked as it is by default.

Of course things can change if you configure it differently from the default setting. For example, one could sync the PostgreSQL password with UNIX password and only allow local logins. That would be beyond the scope of this question.