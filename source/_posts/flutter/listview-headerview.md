---
title: flutter中list view加一个header view
date: 2020-11-20 23:24:35
categories: 
- flutter
tags:
---

```
body:   CustomScrollView(
        slivers: <Widget>[

          SliverGrid.count(
           //具体的配置
          ),
          
          
          //列表
          SliverFixedExtentList(
            delegate: SliverChildBuilderDelegate(
                  (context, index) => ConversationListItem(
                      delegate: this, conversation: conList[index]
                  ),
              childCount: conList.length,
            ),
            itemExtent: 100,
          ),
        ],
      ),
```

解析：大的容器叫做custom scroll view,子控件叫做slivers，是一个数组，在数组里面从上到下排布sliver控件，有sliver grid，有sliver fixed extent list

- 效果大概长这样![image](https://img-blog.csdnimg.cn/20191101164249461.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dvcnNoaXBfS2lsbA==,size_16,color_FFFFFF,t_70)