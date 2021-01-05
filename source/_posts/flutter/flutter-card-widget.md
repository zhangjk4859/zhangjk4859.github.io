---
title: flutter card组件
date: 2021-01-05 10:27:30
categories: 
- flutter
tags:
---

在开发过程中，Container组件使用多了，会有一些重复的代码，比如矩形边框和圆角，需要额外加decoration,使用card已经默认加上了边框和阴影

```dart
Card(
  margin: EdgeInsets.all(10),
  child: ...
)
```

