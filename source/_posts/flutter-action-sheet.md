---
title: flutter actionSheet使用方法
date: 2020-11-26 18:51:55
tags:
---

```dart
//函数
_showCupertinoActionSheet() async{
    var result = await showCupertinoModalPopup(
        context: context,
        builder: (context) {
          return CupertinoActionSheet(

            title: Text('标题'),
            message: Text('内容'),
            actions: <Widget>[
              CupertinoActionSheetAction(
                child: Text(
                    '标题一',
                  style: TextStyle(
                    color: Color(0xFF00C599)
                  ),
                ),
                onPressed: () {
                  Navigator.of(context).pop('delete');
                },
                isDefaultAction: true,
              ),
              
              CupertinoActionSheetAction(
                child: Text('标题二'),
                onPressed: () {
                  Navigator.of(context).pop('not delete');
                },
                isDestructiveAction: true,
              ),
            ],
            cancelButton: CupertinoActionSheetAction(
              child: Text(
                  '取消',
                style: TextStyle(
                  color: Colors.white
                ),
              ),
              onPressed: () {
                Navigator.of(context).pop('cancel');
              },
            ),
          );
        });
    print('$result');
  }
```

总结：在showCupertinoModalPopup方法里返回CupertinoActionSheet，里面的元素由CupertinoActionSheetAction组成，有default和destructive类型可选，用法和UI和苹果大致一样

![image](https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=2828331492,1718232482&fm=15&gp=0.jpg)