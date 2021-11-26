---
title: 取绝对值？没那么简单
date: 2021-09-17 11:43:48
categories: 
- 计算机
tags:
---

取绝对值，第一印象，正数返回本身，负数取反

```java
public static double abs(double value) {
  if (value < 0) {
    return -value;
  }
  return value;
}
```

函数有什么问题吗？

[IEEE-754](https://en.wikipedia.org/wiki/IEEE_754-2008)标准中，有两种0，+0.0 & -0.0，很容易搞混，但是实际上不一样，不论是在文本呈现方式还是运算过程中。举例来说，





来源：https://habr.com/en/post/574082/
