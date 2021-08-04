---
title: hexo给目录分类
date: 2021-01-05 13:55:10
categories: 
- unix
tags:
---

创建分类功能

```shell
hexo new page categories
```

打开index文件

```
/source/categories/index.md
```

文件添加字段

```
title: categories
date: 2021-01-05 12:19:59
type: "categories"
```

写文章的时候加上分类标签

```
title: mac android studio flutter 打包 apk
date: 2020-11-16 20:16:07
categories: 
- unix
tags:
```

添加标签同理

完。

参考：https://www.cnblogs.com/hankleo/p/11606224.html