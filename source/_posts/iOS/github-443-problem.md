---
title: pod下载三方库github 443问题
date: 2021-04-28 09:59:55
categories: 
- iOS
tags:
---

报错原文：

```shell
Cloning into '/var/folders/nd/n2mbp09n1lqbyyf586wntcww0000gn/T/d20210428-5764-pwxnoe'...
fatal: unable to access 'https://github.com/SDWebImage/SDWebImage.git/': LibreSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443 
```

原因分析：

>  本地git使用代理连接github，代理出了问题

问题解决：

> 让代理恢复正常或者不使用代理

```shell
git config --global --unset http.https://github.com.proxy
git config --global --unset https.https://github.com.proxy
```

> 去除了http 和 https的代理

完。

参考：https://www.jianshu.com/p/388c2914f22a