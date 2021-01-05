---
title: flutter中radio单选使用
date: 2021-01-05 10:10:26
tags:
---

在一个数组容器里放置两个及其以上radio，当radio的group value和自己value相等时，便是选中状态

```dart
int groupValue = 1;
_onChange(value){
    if(mounted)
      setState(() {
        groupValue = value;
      });
  }

Row(
             
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        Radio(
          value: 1,
          groupValue: groupValue,
          onChanged: (T) => _onChange(T),
        ),
        Radio(
          value: 2,
          groupValue: groupValue,
          onChanged: (T) => _onChange(T),
        ),
        Radio(
          value: 3,
          groupValue: groupValue,
          onChanged: (T) => _onChange(T),
        ),
      ],
        )
```

参考：https://blog.csdn.net/zhangwes/article/details/104978660