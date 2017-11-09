---
title: "glide不能下载golang.org/x包的替代方案"
date: 2017年11月 8日 星期三 16时20分51秒 CST
tags: [golang, glide]
author: chenchuanyin
---

> glide是go的一个包管理工具，可以直接扫描工程管理import依赖。而golang.org/x下的包是viper、logrus等github开源包的依赖，国内又不能访问。一个好消息是golang.org/x在github上有镜像(github.com/golang)。下面是我尝试成功的替代方案。

如果go工程中有golang.org/x/net的依赖，就可以在glide.yaml中加入以下配置：
```code
- package: golang.org/x/net
  repo:    https://github.com:golang/net.git
  vcs:     git
```
这样`glide install/update`就可以从github.com镜像中下载相关库了。
