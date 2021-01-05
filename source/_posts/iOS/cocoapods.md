---
title: 2020-11安装cocoapods问题
date: 2020-11-12 18:48:08
categories: 
- iOS
tags:
---
今天安装pods发生无法下载问题，

```
Unable to download data from XXX
```

切换了镜像源解决

- 查看镜像源

```
gem sources -l
```

- 删除淘宝镜像源 -r remove

```
sudo gem sources -r https://ruby.taobao.org/
```

- 添加新的镜像源  -a add

```
sudo gem sources -a https://rubygems.org
```

- 安装
```
sudo gem install cocoapods
```

- 成功
Successfully installed cocoapods-1.10.0
Parsing documentation for cocoapods-1.10.0
Done installing documentation for cocoapods after 2 seconds 

参考：https://blog.csdn.net/li_ph/article/details/43852845
