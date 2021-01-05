---
title: zsh的挽救
date: 2020-11-23 18:36:03
categories: 
- unix
tags:
---

今天配置环境变量的时候，因为失误不小心让zsh整个失效了，

```
zsh: command not found:xxx
```

补救办法，在命令行输入

```
PATH=/bin:/usr/bin:/usr/local/bin:${PATH}
```

恢复正常

失误的地方在于配置flutter时路径少输入一个$符号，在$HOME/.zshrc文件中

```
//正确
export PATH="$PATH:[PATH_TO_FLUTTER_GIT_DIRECTORY]/flutter/bin"
//错误
export PATH="PATH:[PATH_TO_FLUTTER_GIT_DIRECTORY]/flutter/bin"
//注意 PATH_TO_FLUTTER_GIT_DIRECTORY 是需要输入全路径的，/User/xxx/xxx,不是~符号！
```

最后一个坑，android studio无法加载应用市场插件，乖乖下载安装包从零开始安装便不会出现问题，不能从别的电脑直接拖过来直接用.

### 完