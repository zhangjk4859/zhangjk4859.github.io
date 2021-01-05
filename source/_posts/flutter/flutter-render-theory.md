---
title: flutter渲染原理要点
date: 2020-12-02 23:35:58
categories: 
- flutter
tags:
---

- 渲染过程会生成三棵树

  - widget树

  - element树

  - render object树

    

- 提高buid效率，在build方法中尽量少做事，层级越简单越好
- setState方法尽量下放到底层节点
- 尽量减少重绘区域，使用repaint boundry
- 减少离屏渲染 比如save layer，clip path，
- 减少透明度使用，因为每一帧都会重建widget
- 建立缓存池
- 提升layout效率

参考：https://www.freesion.com/article/8834628331/

