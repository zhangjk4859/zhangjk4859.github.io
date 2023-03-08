---
title: 微信小程序开发总结
date: 2023-3-8 12:19:21
categories: 
- vue
tags:
---

问题描述：onload函数option参数，小程序二次扫码无法获取更新

解决：使用 ```wx.getEnterOptionsSync()```获取最新参数，冷启动与```App.onLaunch```保持一致，热启动与```App.onShow```保持一致

参考：https://blog.csdn.net/weixin_45575594/article/details/123224076


