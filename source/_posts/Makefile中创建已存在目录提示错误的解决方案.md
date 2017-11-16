---
title: "Makefile中重复创建目录提示错误的解决方案"
date: 2017年11月 8日 星期三 16时48分00秒 CST
tags: [makefile]
author: chenchuanyin
category: 学习
---

如题，我们经常需要在构建脚本Makefile中创建目录。例如下面一段脚本：
```makefile
deps:
	git submodule update --init --recursive
	mkdir -p out

build:
	cd out && cmake -DBUILD_TESTING=OFF ../ && make -j8

package: deps build

clean:
	rm -rf out/*

```
在`out`目录已存在后执行`make deps`，会出现以下错误：
```text
➜  cpp-demo git:(master) ✗ make deps
git submodule update --init --recursive
mkdir out
mkdir: out: File exists
make: *** [deps] Error 1
➜  cpp-demo git:(master)
```
为了消除这个错误提示，我们可以在`mkdir out`加入参数`-p`:`mkdir -p out`。
这样就不会提示错误了。
