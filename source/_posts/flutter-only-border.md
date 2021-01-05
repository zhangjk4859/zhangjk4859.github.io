---
title: flutter个别圆角切割
date: 2021-01-05 10:06:41
tags:
---

取用圆角类的only属性，左上，右上，左下，右下，此处圆角半径也是一个类

```dart
BorderRadius.only(
  topLeft: Radius.circular(8.w),
  topRight: Radius.circular(8.w),
)
```

全部圆角则取all

```dart
BorderRadius.all(
  Radius.circular(8.w)
)
```

