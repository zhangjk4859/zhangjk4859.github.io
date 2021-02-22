---
title: hexo部署文章到github 443问题
date: 2021-2-22 07:45:52
categories: 
- 计算机
tags:
---

问题：

```shell
fatal: unable to access 'https://github.com/xxx/xxx.github.io.git/': LibreSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443 
FATAL {
  err: Error: Spawn failed
      at ChildProcess.<anonymous> (/Users/kevin/Desktop/xxx.github.io/node_modules/hexo-deployer-git/node_modules/hexo-util/lib/spawn.js:51:21)
      at ChildProcess.emit (events.js:315:20)
      at Process.ChildProcess._handle.onexit (internal/child_process.js:277:12) {
    code: 128
  }
} Something's wrong. Maybe you can find the solution here: %s https://hexo.io/docs/troubleshooting.html
```

解决：在_config.yml文件里把deploy的地址从http换成git

```yaml
deploy:
  type: git
  #repo: https://github.com/xxx/xxx.github.io.git
  repo: git@github.com:xxx/xxx.github.io.git
  branch: master

```

