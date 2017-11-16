---
title: "pip国内下载失败超时等问题的解决方案"
date: 2017年11月 8日 星期三 16时48分00秒 CST
tags: [python]
author: chenchuanyin
category: 学习
---

可以通过国内开源镜像来下载python的库,操作步骤如下：
```shell
mkdir ~/.pip
vim ~/.pip/pip.conf
```
pip.conf内容如下：
```text
[global]
index-url = https://pypi.mirrors.ustc.edu.cn/simple
```
