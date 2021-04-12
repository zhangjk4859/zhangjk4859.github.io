---
title: flutter安卓release包代码无法执行
date: 2021-4-11 09:18:49
categories: 
- flutter
tags:
---

## 问题描述：

flutter工程打包apk文件后

```kotlin
            try {
                val method = javaClass.getDeclaredMethod(call.method, MethodCall::class.java, MethodChannel.Result::class.java)
                method.invoke(this, call, result)
            } catch (e: NoSuchMethodException) {
                e.printStackTrace()
            } catch (e: IllegalAccessException) {
                e.printStackTrace()
            } catch (e: InvocationTargetException) {
                e.printStackTrace()
            }
```

这段代码无法执行

## 原因分析

经过咨询，安卓release包会代码混淆，使用反射会让代码无法精确匹配

## 解决:

- 使用反射的类不参与混淆，降低安全性
- 不使用反射，改用if判断或者switch case



参考：1. https://stackoverflow.com/questions/41525867/reflection-not-working-on-android-release-apk-even-with-proguard-minify-disable

2.https://blog.csdn.net/guohesheng/article/details/53696652

3.https://www.jianshu.com/p/b5b2a5dfaaf4

感谢王志浩同学提供帮助！