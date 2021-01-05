---
title: dart枚举
date: 2020-12-02 08:03:53
categories: 
- flutter
tags:
---

```dart
enum MediaType {
  movie,      //0
  shortVideo, //1
  other,      //2
}

var videoType = MediaType.values[0];
// videoType == movie

```

定义枚举和OC差别不大，取值的时候不可以直接和int比较，需要从枚举数组中根据index拿出来，比OC多了一步