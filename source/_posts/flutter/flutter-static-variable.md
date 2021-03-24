---
title: flutter无法访问另一个类的全局变量
date: 2021-3-2 10:50:49
categories: 
- flutter
tags:
---

错误描述:在A类访问B类里的static 变量，永远是初始值，即使已经设置过新值

解决办法：A类import B类头文件时使用绝对路径，不使用系统默认

```shell
//错误
import 'package:xxx_app/utils/app_helper.dart';
//正确
import '../utils/app_helper.dart';
```

B类结构

```
class AppHelper {
  static String name = "";
  
  someFunction(){
    name = "testName";
  }
}
```



参考：https://stackoverflow.com/questions/45772318/flutter-dart-static-variables-lost-keep-getting-reinitialized

新词：

```
toy around
```

