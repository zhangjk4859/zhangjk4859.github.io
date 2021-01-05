---
title: flutter ListTitle组件
date: 2021-01-05 10:34:14
tags:
---

该组件可以用在container和card组件里，默认有大标题和小标题属性，无需再进行text上下排列组合

```dart
          Card(
            margin: EdgeInsets.all(10),
            child: Column(
              children: <Widget>[
                ListTile(
                  title: Text("张三",style: TextStyle(fontSize: 28)),
                  subtitle: Text("董事长"),
                ),
                Divider(),
                ListTile(
                  title: Text("电话:123456789"),
                ),
                ListTile(title: Text("地址：xxxxxxxxxxxxxxxxx"))
              ],
            ),
          ),
```

