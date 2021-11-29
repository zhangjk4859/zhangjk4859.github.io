---
title: jenkins安装失败
date: 2021-11-29 14:37:56
categories: 
- unix
tags:
---

今日安装jenkins，出现报错

```shell
arch -arm64 brew install jenkins
==> Downloading https://mirrors.ustc.edu.cn/homebrew-bottles/bottles/openjdk%4011-11.0.10.arm64_big_sur.bottle.1.tar.gz
#=#=#                                                                         
curl: (22) The requested URL returned error: 404 
Warning: Bottle missing, falling back to the default domain...
==> Downloading https://ghcr.io/v2/homebrew/core/openjdk/11/manifests/11.0.10-1
Already downloaded: /Users/kevin/Library/Caches/Homebrew/downloads/c92dbb3dbfa86fe1cdbe7a74ec208c3789d188d92be2d580af208aef5b80a197--openjdk@11-11.0.10-1.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/openjdk/11/blobs/sha256:8990371b4279802b949bcff3a2064ea0a51e7a64da7449267a1c4021e2d7d6d8
Already downloaded: /Users/kevin/Library/Caches/Homebrew/downloads/92754dc32a66d4a7c38ea48c4e3820236bf633e1bd5949f96cd13a502a14f41f--openjdk@11--11.0.10.arm64_big_sur.bottle.1.tar.gz
==> Downloading https://mirrors.ustc.edu.cn/homebrew-bottles/bottles/jenkins-2.302.all.bottle.tar.gz
#=#=#                                                                         
curl: (22) The requested URL returned error: 404 
Warning: Bottle missing, falling back to the default domain...
==> Downloading https://ghcr.io/v2/homebrew/core/jenkins/manifests/2.302
Already downloaded: /Users/kevin/Library/Caches/Homebrew/downloads/a7cf18dfe095a4d331d7905c74417d764e90ace995b98a023bfae85aced3cb0f--jenkins-2.302.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/jenkins/blobs/sha256:fc7f49175e23a67127dc70338bd12abac822048f12b213fc666e1f9499ff6e82
Already downloaded: /Users/kevin/Library/Caches/Homebrew/downloads/eb6411ff42c44cb186e34607b5ac9d17d67777a07a985ad36570e9001354fae7--jenkins--2.302.all.bottle.tar.gz
==> Installing dependencies for jenkins: openjdk@11
==> Installing jenkins dependency: openjdk@11
==> Pouring openjdk@11-11.0.10.arm64_big_sur.bottle.1.tar.gz
tar: Error opening archive: Failed to open '/Users/kevin/Library/Caches/Homebrew/downloads/1096bb647c4eefa040e362e9f88af881902e3cfd88dc4bb9daab7319cda7ab44--openjdk@11-11.0.10.arm64_big_sur.bottle.1.tar.gz'
Error: Failure while executing; `tar --extract --no-same-owner --file /Users/kevin/Library/Caches/Homebrew/downloads/1096bb647c4eefa040e362e9f88af881902e3cfd88dc4bb9daab7319cda7ab44--openjdk@11-11.0.10.arm64_big_sur.bottle.1.tar.gz --directory /private/tmp/d20211129-8757-13q6qjl` exited with 1. Here's the output:
tar: Error opening archive: Failed to open '/Users/kevin/Library/Caches/Homebrew/downloads/1096bb647c4eefa040e362e9f88af881902e3cfd88dc4bb9daab7319cda7ab44--openjdk@11-11.0.10.arm64_big_sur.bottle.1.tar.gz'

```

解决方案

```shell
export HOMEBREW_BOTTLE_DOMAIN=''
arch -arm64 brew install jenkins
```

分析：

```shell
open ~/.zprofile
export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles/bottles #ckbrew
  eval $(/opt/homebrew/bin/brew shellenv) #ckbrew
```

可以看到是中科大的镜像，未和官网完成同步，五月一号起官网已不再支持bintray服务，把域名切换为空即可

完。

参考：https://www.tinkol.com/372
