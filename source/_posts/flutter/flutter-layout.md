---
title: flutter基础知识
date: 2020-11-17 17:38:24
categories: 
- flutter
tags:
---
基本上由widget组成，widget有stateless和stateful两种，常用的基础widget有
- container：矩形元素，可以设置背景边框阴影
- row，column：让子控件水平和垂直布局，flex布局原理
- stack：可以堆砌widget，用上下左右来定位
- text：一个文本显示容器

多功能widget叫做material app widget，苹果风格的叫做CupertinoApp，常见的有：
- navigator，也叫routes
- appbar
- scaffold



---
- 一个widget加gestureDetector便形成了按钮
- 一个widget+state = statefull widget
- keys：类似于tableview中的cellid，重用机制
- 全局key：用来标识全局唯一的widget


关于widget组合的图：
![image](https://flutter.cn/assets/ui/layout/lakes-icons-visual-f9e45691d76ba85d4ea2160941f42c8a2ce1a17d41d6e6aac8f3feb89e679f99.png)
![image](https://flutter.cn/assets/ui/layout/sample-flutter-layout-46c76f6ab08f94fa4204469dbcf6548a968052af102ae5a1ae3c78bc24e0d915.png)

参考：https://flutter.cn/docs/development/ui/layout
