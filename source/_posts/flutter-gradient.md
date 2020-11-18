---
title: flutter渐变处理
date: 2020-11-18 12:20:54
tags:
---
- 线性渐变
- 开始位置
- 结束位置
- 开始结束点
- 颜色
```
LinearGradient(      //渐变位置
              begin: Alignment.topLeft, //左上
              end: Alignment.bottomRight, //右下
              stops: [0.0, 1.0],         //[渐变起始点, 渐变结束点]
              //渐变颜色[始点颜色, 结束颜色]
              colors: [Color.fromRGBO(253, 1, 129, 1), Color.fromRGBO(206, 21, 240, 1)]
          )
```
