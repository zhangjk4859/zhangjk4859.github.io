---
title: 更换mac java版本
date: 2021-11-30 10:09:42
categories: 
- unix
tags:
---

电脑默认安装java 16，需要更换为java 8

```shell
open /Library/Java/JavaVirtualMachines/
```

选择想要删除的版本，输入管理员密码

点击[下载java8](https://www.azul.com/downloads/?version=java-8-lts&os=macos&architecture=arm-64-bit&package=jdk)dmg安装

 ```shell
 java -version
 openjdk version "1.8.0_312"
 OpenJDK Runtime Environment (Zulu 8.58.0.13-CA-macos-aarch64) (build 1.8.0_312-b07)
 OpenJDK 64-Bit Server VM (Zulu 8.58.0.13-CA-macos-aarch64) (build 25.312-b07, mixed mode)
 ```

完。

参考：https://www.anotheriosdevblog.com/installing-homebrew-and-jenkins-on-my-m1-mac-mini/