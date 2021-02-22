---
title: framework not found
date: 2021-02-22 16:04:55
categories: 
- iOS
tags:
---

问题：在build的时候framework not found

解决：

- 添加需要的framework
- 确定framework齐全的情况下，就是系统添加了冗余的framework编译需求，找到require列表删除即可

```
project.xcodeproj文件--->显示包内容--->project.pbxproj文件 全局查找删除
```

ps:版本对不上处理方法同理，修改版本号和实际pods下载过来一致