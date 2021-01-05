---
title: pubspec.lock坑
date: 2020-11-25 09:27:09
categories: 
- flutter
tags:
---

昨天以为pubspec.lock文件和cocoapods的profile.lock文件性质一样，可以生成，所以删除，结果遇见了编译报错，即使在执行了

```
flutter pub get
```

命令重新生成后，经过一番研究和队友协助，找到是这个问题，把老的恢复回来工程编译正常，下面是报错的关键字

```
Execution failed for task ':app:processDebugManifest'. > Manifest merger failed : Attribute provider...
```

做记录方便以后查阅。