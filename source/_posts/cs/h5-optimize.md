---
title: h5优化策略总结
date: 2021-02-18 09:14:36
categories: 
- 计算机
tags:
---

- ### 原生webview加载耗时

  - 预热webview，并且缓存多个对象进行复用

- ### webview网络请求页面内容，下载html

  - 在未点开网页时，用网络请求框架异步请求html内容，保存到本地缓存框架中
  - 在移动端启动local web server，同步服务器资源到本地，h5链接替换成localhost+port链接，例如swift版本的Telegraph
  - 本地网络框架请求zip资源并解压，供WKWebview的WKURLSchemeHandler拦截网络请求并调用(例如把http替换为自动以scheme)

- ### 解析html

  - webview请求网络前先本地缓存查找已经下载好的html内容，直接进行加载渲染

- ### 请求js、css资源

  - 本地网络框架选择性下载较大图片文件

- ### 正常页面加载顺序为拿到html，计算布局，识别外链资源，绘制渲染

  - 后端直接加载好页面依赖的css，js和接口数据，拼接好一个最终版html返回给前端

- ### 接口耗时长 

  - 更新接口的处理方式
  - 增加占位图，优化体验

- ### 内存泄露

  - 及时释放图片和数组等资源





参考链接：

- https://tech.youzan.com/h5performancetest
- https://luyanan.com/news/info/19764028651650.html