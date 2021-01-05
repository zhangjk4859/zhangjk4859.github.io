---
title: 面试官想要知道的我的信息
date: 2020-11-18 15:46:46
categories: 
- 杂谈
tags:
---
### 项目开发过程中用到的三方库有哪些
- Masonry  布局
- YYModel  json转模型
- YYCache  缓存工具
- AFNetworking  网络请求
- SDWebImage   图片缓存
- YBAttributeTextTapAction  label特定的字体点击

### 对你们公司有什么想问的
- 前端人员配置如何，iOS端用什么语言
- 后端用的什么语言
- 产品是2B还是2C

### 动态库和静态库区别是什么
- 静态库在编译时链接，锁定在可执行文件中，不会改变，如果库有变更，需要重新编译，不具有共享性
- 动态库在运行时链接，独立于可执行文件，库改变后，无需重新链接即可使用新功能，可以独立存在，具有共享性
- 额外：苹果禁止开发者提供动态库，防止作弊
>参考：https://medium.com/@StueyGK/static-libraries-vs-dynamic-libraries-af78f0b5f1e4#:~:text=Static%20libraries%2C%20while%20reusable%20in,a%20program%20at%20compile%20time.&text=In%20contrast%2C%20a%20dynamic%20library,library's%20files%20at%20compile%2Dtime.
![image](https://tse3-mm.cn.bing.net/th/id/OIP.pURY0S7FKaaGn-N_3AWFNwHaEe?pid=Api&rs=1)


### 关于IP
- internet protocol
- 定义计算机之间如何发送数据包
- 可以把包发送给指定的计算机
### 关于TCP
- transmission control protocol
- 建立网路对话
- 保持网络对话
- 和IP协议协作
- 发送包的基础上保证包传输的完整性，准确性
- 发送的时候把数据拆分成小数据包
- 接收方根据规则组装完整的包
- 在传输过程中包丢失或者错误，会要求重传，保证数据完成性，这样的结果是数据有很高的滞后性（latency）
- 用到TCP的协议有
  - SSH: SecureShell
  - FTP: File Transfer Protocol
  - Telnet: for peer-to-peer file sharing
  - SMTP: simple mail transfer protocol
  - POP: post office protocol
  - IMAP: internet message access protocol
  - HTTP: hyper text transfer protocol

![image](https://tse3-mm.cn.bing.net/th/id/OIP.O6xcvDO-35bKVX47nh2UoAHaEY?pid=Api&rs=1)

- open system interconnection communication model
  - application
  - presentation
  - session
  - transport
  - network
  - data link
  - phycial

- ![image](https://cdn.ttgtmedia.com/rms/onlineImages/networking-osi_vs_tcp-ip_model_table_desktop.jpg)

### 关于UDP
- user data protocol
- 跟TCP相比，仅仅是忽略了应用层用来检测错误细节的数据包
- 比tcp滞后性好
- header包含的信息更少
- 在传输层的信息更少


### NSOperationQueue
- 设置依赖关系
- 最大并发量
- 优先级
- GCD的封装

### GCD
- async开线程
- sync不开线程，在当前线程立即插入执行
- 串行队列 任务依次执行，有严格的顺序，FIFO
- 并发队列 任务并行，不在乎顺序
### 锁
- sychronize(obj){}
- 自旋锁 性能高，盲等
- 互斥锁 性能低，不忙等

### K线图是怎么画上去的
- 在drawrect方法里，调用Core Graphics库
- 获取上下文Context
- 设置线的颜色setStrokeColor
- 设置线的宽度setLineWidth
- 移动到某个点 MoveToPoint
- AddLineToPoint 添加线
- strokePath 划线
- strokeLineSegments 画线段
- setLineCap 线顶端的形状

### http
- get
  - 一个tcp数据包，包含header和data
  - url长度有限制
  - 重复请求被缓存
- post
  - 两个tcp数据包
  - 参数在body中，不会被缓存
  - 重复请求不会被缓存

### OC 给nil发消息会怎么样？为什么
### runtime有哪些应用场景
### 用过js core吗
### socked了解吗？既然在tcp层上，为什么还需要ip和端口号
### YYCACHE 原理是什么
### LRU算法原理是什么
### 你个人最擅长什么
### runloop
### 热更新的原理是什么



### 大项目如何规范重构
### NSString和string的区别是什么
### swift 函数参数可修改，修饰符是什么
### token快到期后如何实现自动登录延期的
### 域名是怎么保证安全，没有被重定向
### websocket如何保证并发
### swift修饰符有了解吗
### 视频传输协议一对一，多对多有了解吗
### 物联网有哪些协议
### 波浪动画是如何实现的
### 不使用https，在http协议下还有办法实现数据安全吗
### 如何实现大文件上传
### 如何给webview加夜间模式
### weak什么时候使用，view will appear需要加weak吗？
### sdwebimage是什么原理，图片key是如何存储的
### 一个像素宽度的线是怎么画出来的
### 原生如何传给h5图片
### 贝塞尔曲线如何画坐标与弧线的
### UIWebview如何避免内存泄露
### bugly是什么原理实现的
### 项目如何模块化？pods?
### 单例是什么原理
### 音视频开发过吗？
### K线图是如何刷新的
### 你是如何学习一门新技术的
### 数据库了解吗？
### 如何优雅的断开TCP连接
### KVC是什么原理
### tableView如何优化
### 用过react吗？
### 多线程有哪些使用场景
### block有几种类型

- 栈上block NSConcreteStackBlock

- 堆上block  栈上block做了copy以后  NSConcreteMallocBlock

- 全局block NSConcreteGlobeBlock 存储在全局数据区

  总结：block是对象，一般情况下，对象经常呆的也就是这三个区，对于基础类型，会进行拷贝，对象会默认进行强引用，如果__block修饰过的数据类型，会包装一个指针，指向变量

### 如何检测内存的占用情况
### 常用的本地存储有哪些
### 在项目中做了哪些优化
### RAC是什么原理
### 性能检测用过吗？
### NSConditionLock，wait和lock区别是什么
### WKWebview缓存如何使用
### WKWebview和Uiwebview有什么区别
### 常用的锁有哪几种
### AutoReleasePool原理是什么
### 常见的崩溃有哪些？
### sync开线程吗？
### 设计模式有哪些？
### HTTPS如何保证文件的完整性 没有被篡改？
### 工厂模式又细分为哪些模式
### app的加密安全性了解过吗
### 了解哪些设计原则
### 工程有哪些优化，fastlane证书配在哪里
### 链表了解吗，双向链表是什么，跟数组的区别，数组为什么快
### weak原理能讲下吗，assign区别是什么
### 工程里具体的设计模式

### srwebsocket用的什么协议

### 客户端如何做好网络请求管理 减少服务器的压力

### 客户端如果被破解了怎么办？加密方式怎么处理

### 本地存储有用数据库吗

### leetcode第一题有更优的解法

### IM负载多少？

### 客户端如何实现https的

### 服务端如何处理大量网路访问请求

### ios断点续传原理
- 工厂模式+ 切片 + 多种文件格式怎么处理 + 长连接


待处理信息：
> 1.尽量减少宏的使用，使用全局C语言函数返回值
2.打包一次，随意切换环境
3.用jenkins把打包权限给到对方，彻底不用再打包 fastlane+fir
4.减少资源，动态库，适当多线程使用，load延迟到initialize
5.runtime模块化，抽取与封装
6.懒加载思想，单一职责
7.设计模式：工厂  父类指针指向子类对象  
http:完整性 链表，断点续传 发编译
单例
代理  解耦  一对一
观察者   一对多
MVC  MVVM  职责不同
