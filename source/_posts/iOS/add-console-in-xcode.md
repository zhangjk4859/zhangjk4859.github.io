---
title: open terminal in Xcode
date: 2021-11-25 14:06:27
categories: 
- iOS
tags:
---

用惯了Android Studio底部直接可以用terminal，在想Xcode是不是可以有类似功能，经过查询，整理出方法

- 新建一个.sh文件，内容如下，保存

```shell
#!/bin/bash

open -a Terminal "`pwd`"
```

- 打开Xcode--->Preference--->Behaviors--->Custom--->Run,选择创建好的.sh文件，Run前面的checkbox打钩，设定一个快捷键，这样，在Xcode界面使用快捷键就可以打开当前文件夹的终端窗口了。

完。

参考：https://stackoverflow.com/questions/21998706/terminal-window-inside-xcode
