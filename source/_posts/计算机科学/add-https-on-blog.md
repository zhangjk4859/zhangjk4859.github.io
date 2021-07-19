---
title: 给自己的博客域名加https
date: 2021-07-19 09:51:15
tags:
---

​    一开始想添加一个博客评论系统，方便交流，参考的是[kid的博客](https://freemind.pluskid.org/technology/github-based-comment-system-and-the-death-of-independent-blog/)，选择最简单的方案 [utteranc.es](https://utteranc.es/)，hexo已经有[插件集成](https://zhuanlan.zhihu.com/p/76237379)，使用的是npm安装。安装完成后在博客底部成功出现评论框



点击github登录时出现了访问失败，找不到资源

![image](https://github.com/zhangjk4859/zhangjk4859.github.io/blob/zjk/pics/domain404.jpg?raw=true)

经过测试，确定原因是自己域名没有https的原因，链接添加参数后默认以https访问出现请求失败情况。首先想到的是去阿里万网看自带的服务，价格有些小贵![image](https://github.com/zhangjk4859/zhangjk4859.github.io/blob/zjk/pics/wanwangprice.png?raw=true)



为了秉持互联网免费原则，确定了[Netlify方案](https://jaeger.itscoder.com/web/2017/08/30/github-page-https.html),根据教程配置完成后大概等了半天时间，https域名就可以正常使用了。

没有尝试的方案：

- [阿里云一年免费](https://blog.csdn.net/zaq0123/article/details/79880838)
- [cloud flare免费方案](https://tzhou2018.github.io/2018/04/%E4%B8%BAGitHub-Pages%E8%87%AA%E5%AE%9A%E4%B9%89%E5%9F%9F%E5%90%8D%E5%B9%B6%E6%B7%BB%E5%8A%A0SSL-%E5%BC%80%E5%90%AFHTTPS%E5%BC%BA%E5%88%B6/)

感谢[蓝伟洪](https://blog.lanweihong.com/posts/24011/)和[小蘑菇](https://yanqizhao.com/)配合测试评论系统。

