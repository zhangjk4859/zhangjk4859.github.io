---
title: jenkins安装
date: 2021-01-20 10:33:31
categories: 
- unix
tags:
---

- 安装

  ```
  brew install jenkins-lts
  ```

- 启动

  ```shell
  brew services start jenkins-lts
  ```

- 停止

  ```shell
  brew services stop jenkins-lts
  ```

- 重启

  ```shell
  brew services restart jenkins-lts
  ```

- 更新

  ```shell
  brew upgrade jenkins-lts
  ```

  

局域网访问配置

``homebrew.mxcl.jenkins.plist``里面``httpListenAddress``从``127.0.0.1``更改为``0.0.0.0``

两个地方

- ` ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist`
- `/usr/local/Cellar/jenkins/版本号/homebrew.mxcl.jenkins.plist`

参考：https://www.jianshu.com/p/10041e79ac6f