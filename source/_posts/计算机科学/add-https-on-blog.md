---
title: 给自己的博客域名加https
date: 2021-07-19 09:51:15
tags:
---

​    一开始想添加一个博客评论系统，方便交流，参考的是[kid的博客](https://freemind.pluskid.org/technology/github-based-comment-system-and-the-death-of-independent-blog/)，选择最简单的方案 [utteranc.es](https://utteranc.es/)，hexo已经有[插件集成](https://zhuanlan.zhihu.com/p/76237379)，使用的是npm安装。安装完成后在博客底部成功出现评论框，点击github登录时出现了访问失败，找不到资源，经过测试，确定原因是自己域名没有https的原因，链接添加参数后默认以https访问出现请求失败情况。首先想到的是去阿里万网看自带的服务，价格有些小贵，

