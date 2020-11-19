---
title: flutter按钮点击事件传给delegate
date: 2020-11-19 22:43:34
tags:
---
在ios中，通常用block或者代理去实现，在flutter中，外部实现一个方法，把这个方法传给按钮，按钮内部用callback接受，ontap方法调用即可，实现如下

```
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

//定义函数类型
typedef StringValue = void Function(String);

class ImageBtn extends StatelessWidget {
 //作为属性
  StringValue callback;

  ImageBtn({Key key,this.callback}) : super(key: key);

  @override
  Widget build(BuildContext context) {
   
    return new GestureDetector(
      onTap: () {
        print('MyButton was tappedq!');
        //调用
        this.callback("testString");
      },
      child: ...
      ),
    );
  }
}
```
外部使用方法

```
  //顶部按钮点击事件
  void _ontap(String name){
    print(name);
  }
  //实例对象时传进去
  ImageBtn(callback:_ontap)
```
注意:callback和外部的方法，参数类型要保持一致
总结：外部函数传给按钮，让按钮内部可以调用
