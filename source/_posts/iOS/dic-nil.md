---
title: 字典取值为空崩溃问题
date: 2020-11-13 10:24:39
categories: 
- iOS
tags:
---
今天后台报错
```
[_NSPlaceholderData initWithBase64Encoding:]: nil string argument
Foundation	-[NSData(NSData) base64Encoding]
```
经过检查问题发生在字典取出值没有判空就传递给方法使用，细节也要注意，养成良好的编码习惯
```
NSString *urlstr = dic[@"imgBase64"];
NSData *data = [[NSData alloc] initWithBase64Encoding:urlstr];
```
正确的代码

```
id obj = dic[@"imgBase64"];
if (obj && [obj isKindOfClass:[NSString class]]) {
    NSString *urlstr = (NSString *)obj;
    NSData *data = [[NSData alloc] initWithBase64Encoding:urlstr];
}
```
