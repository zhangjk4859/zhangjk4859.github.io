---
title: fijkplayer播放期间屏幕熄灭处理
date: 2020-11-25 23:49:43
categories: 
- flutter
tags:
---

两种方案

1.借用第三方插件，让当前页面保持常量，别的页面跟随系统

```
wakelock: ^0.1.4+2

Wakelock.enable();
Wakelock.disable();
```

2.调用fijkplayer自身的常量参数 二选一

```
await player.setOption(FijkOption.hostCategory, "request-screen-on", 1);
FijkPlugin.keepScreenOn ;
```

参考：https://www.jianshu.com/p/8750de450850

https://fijkplayer.befovy.com/docs/zh/host-option.html#gsc.tab=0