---
title: flutter控件从上到下居中排列
date: 2020-11-19 22:30:23
tags:
---

```
Column(
          children: <Widget>[
            Expanded(child:
            Image.asset('assets/images/$imageName.png')
            ),
            
            Text(
              this.model.title,
              style: TextStyle(
                fontSize: 15,
                color: Colors.white,
              ),
            ),
          ],
        ),
```
注解：
- column是一个垂直的容器，子控件放在children里面
- 要想让图片居中，需要放在expanded容器里面,官方定义：expanded is a widget that expands a child of a row,column,or flex so that the child fills the available space.
- ![image](https://flutter.github.io/assets-for-api-docs/assets/widgets/expanded_column.png)
