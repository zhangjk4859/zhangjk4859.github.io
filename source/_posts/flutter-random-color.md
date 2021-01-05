---
title: flutter随机颜色生成
date: 2021-01-05 10:00:03
tags:
---

在listview或gridview中，用index去获颜色，挨个取一遍

```dart
Colors.primaries[index % Colors.primaries.length]
```

