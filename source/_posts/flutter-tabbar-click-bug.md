---
title: flutter tabcontroller监听点击调用两次
date: 2020-11-18 16:14:48
tags:
---
原因：点击本身出发一次监听，随之产生的动画效果再次出发监听，如果是滑动，仅触发一次监听
解决：看下点击的索引和动画值对不对，过滤掉点击的listen，只显示动画的listen
```
_tabController.addListener(() {
      if(_tabController.index == _tabController.animation.value){
        int index = _tabController.index;
        print("====================当前点击了$index===============");
      }

    });
```
代码拿过来自己分析一遍会记得牢。
