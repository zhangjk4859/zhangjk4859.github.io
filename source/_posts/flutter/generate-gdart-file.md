---
title: flutter模型生成
date: 2020-12-25 13:17:10
categories: 
- flutter
tags:
---

首先自己写好模型类模板代码

```dart
import 'package:json_annotation/json_annotation.dart';
part 'buy_record_data.g.dart';

///标志class需要实现json序列化功能
@JsonSerializable()
class BuyRecordData {
  ///属性
  List<BuyRecordEntity> entities;
  /// 构造函数
  BuyRecordData(this.entities);
  /// 这个函数在.g.dart中，命名就是类名+FromJson
  /// 直接写就行 报错也没关系 生成.g.dart文件之后就好了
  factory BuyRecordData.fromJson(Map<String, dynamic> json) =>
      _$BuyRecordDataFromJson(json);
  Map<String, dynamic> toJson() => _$BuyRecordDataToJson(this);
}
```

然后在终端运行，生成.g.dart文件

```
flutter packages pub run build_runner build --delete-conflicting-outputs

```

参考：1. https://blog.csdn.net/YoYo_Newbie/article/details/90634878?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromBaidu-1.control&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromBaidu-1.control

2. https://my.oschina.net/u/4326108/blog/3675231