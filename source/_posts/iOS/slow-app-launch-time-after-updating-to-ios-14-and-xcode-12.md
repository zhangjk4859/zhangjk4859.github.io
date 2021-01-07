---
title: Xcode12,iOS14，app启动慢
date: 2021-01-07 12:38:38
categories: 
- iOS
tags:
---

问题：启动app会白屏很长一段时间，即使是一个全新的app

解决方案：

- In the Xcode menu,go to product > scheme > edit scheme
- open the info tab
- Uncheck the debug executables checkbox

参考：1. https://stackoverflow.com/questions/63929122/slow-app-launch-time-after-updating-to-ios-14-and-xcode-12

2.https://developer.apple.com/forums/thread/651012