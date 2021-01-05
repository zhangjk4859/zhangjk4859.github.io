---
title: flutter padding组件
date: 2021-01-05 10:43:56
categories: 
- flutter
tags:
---

如果一个组件没有调整内边距的属性，那么可以在它的外层加一层Padding，达到调整位置的效果，效果等同于放到Container里，比Container更轻量级

```dart
Padding(
  padding: EdgeInsets.all(10),
  child: Text('这是一段测试文字'),
)
```

