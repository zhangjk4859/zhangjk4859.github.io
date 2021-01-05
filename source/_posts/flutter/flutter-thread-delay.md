---
title: flutter延迟执行方法
date: 2020-11-18 12:21:12
categories: 
- flutter
tags:
---
延迟加载

```
//延迟1秒加载
Future.delayed(Duration(seconds: 1), (){
      //do sth
    });
```
使用场景：
> 同时执行toast和导航栏页面切换，会导致卡顿，可用延迟其中一个方法，避免同时执行
