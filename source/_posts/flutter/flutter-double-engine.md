---
title: flutter安卓开启第二引擎跑网页
date: 2021-7-2 11:43:01
categories: 
- flutter
tags:
---

​    在纯flutter应用里打开网页，目前流行两个插件:

-  [flutter_webview_plugin](https://pub.flutter-io.cn/packages/flutter_webview_plugin) (以下简称**三方web**)

  - 特点

    >1.实测中滑动相对流畅
    >
    >2.bug较少
    >
    >3.不在flutter的widget tree中，视图在app最顶层，通过channel通知来实现显示和隐藏，全局是一个单例
    >
    >4.非官方

- [webview_flutter](https://pub.flutter-io.cn/packages/webview_flutter)(以下简称**官方web**)

  - 特点

    > 1.镶嵌在widget tree中，方便在flutter中控制
    >
    > 2.键盘弹出有部分bug
    >
    > 3.官方支持

由于历史原因和开发成本考虑，继续沿用三方web作为浏览器，遇到一个需求，就是需要打开网页的时候秒开，实现类似[今日头条的效果](https://blog.csdn.net/zhenghhgz/article/details/112302985)，经过调研和结合flutter特性，最终方案定型为下图

