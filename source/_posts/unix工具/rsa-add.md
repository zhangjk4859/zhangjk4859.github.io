---
title: ssh避免重复输入密码
date: 2021-01-20 11:52:44
categories: 
- unix
tags:
---

解决方法：添加私钥

步骤：

- 切换到文件夹

```shell
cd ~/.ssh
```

- 添加秘钥

```shell
ssh-add id_rsa          
```

- 查看秘钥

```
ssh-add -l
```

- 测试github仓库连接

```
git ls-remote -h -- git@github.com:zhangjk4859/jenkins-build-iOS.git
```

完。

参考：https://superuser.com/questions/988185/how-to-avoid-being-asked-enter-passphrase-for-key-when-im-doing-ssh-operatio