---
title: flutter网络三方库Flutter-Net
date: 2021-01-05 10:54:40
categories: 
- flutter
tags:
---

在给app的网络请求添加loading过程中，发现一个封装更加完善的网络三方库，里面有很多值得借鉴的细节，特此记录

优点：

- 默认自带loading，如果单个请求不想要loading，可以传递参不显示，自己封装的目前全部显示loading
- 更加友好的控制台json打印
- 封装了公共参数
- 响应拦截

来源：https://github.com/po1arbear/Flutter-Net