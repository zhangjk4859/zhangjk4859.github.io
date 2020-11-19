---
title: flutter判断页面是否在屏幕上
date: 2020-11-19 22:18:51
tags:
---
```
ModalRoute.of(context).isCurrent
```
解析：由于页面的组合都是由路由管理的，所以把当前的context传给路由，让路由去判断是否在最顶端，这个路由叫做模态路由
