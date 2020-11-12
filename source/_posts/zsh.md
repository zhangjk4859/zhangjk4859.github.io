---
title: catalina系统的zsh配置
date: 2020-11-12 18:13:26
tags:
---
catalina系统默认的终端是zsh，如果没有找到配置文件，需要自己创建

```
vim ~/.zshrc
```
保存运行使之生效

```
source $HOME/.zshrc
```

看一下是否成功

```
echo $PATH
```
参考：https://stackoverflow.com/questions/10574684/where-to-place-path-variable-assertions-in-zsh
