---
title: flutter pub get慢
date: 2020-11-12 19:30:00
categories: 
- flutter
tags:
---
- 分析：从开发者仓库网站下载依赖比较慢，网络问题
- 解决：
更换数据源地址

```
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
```
最后翻墙运行

- 参考：https://www.askmaclean.com/archives/flutter-pub-get-slow.html
