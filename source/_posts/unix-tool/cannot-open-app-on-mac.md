---
title: 无法打开"xxx",因为无法确认开发者的身份
date: 2020-11-25 23:55:41
categories: 
- unix
tags:
---

处理方法

- 加权限,同意任何来源

```
sudo spctl --master-disable
//用完还原
sudo spctl --master-enable
```

- 按住command键，鼠标右键菜单选择打开app，出现窗口会出现打开按钮，正常情况下不会出现

  ![image](https://huajiakeji.com/Content/kindeditor/attached/image/20190725/20190725213552_3966.png)

  参考：https://huajiakeji.com/macos/2019-07/2793.html

完。