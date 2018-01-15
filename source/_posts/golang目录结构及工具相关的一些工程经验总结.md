---
title: "golang目录结构及工具相关的一些工程经验总结"
date: 2017年11月16日 星期四 11时15分37秒 CST
tags: [golang]
author: chenchuanyin
category: 学习
---

> 在开发golang组件的时候需要版本管理及组件管理，自己形成了一套模式框架，对于常规项目开发可以方便套用。

### 工具
* 使用glide工具进行第三方版本包管理，不用依赖环境变量$GOPATH
* 使用makefile作为脚本工具，管理下载三方包，构建，打包
* 使用emacs+gocode来进行代码编写

### 目录结构


```text
.
├── Makefile       :脚本
├── bin            :组件产物输出目录，不用进行版本管理
├── conf           :配置脚本
├── glide.lock     :glide生成的文件
├── glide.yaml     :glide生成的文件
├── pkg            :gocode需要根据这个目录.a文件进行自动补全
├── src            :源代码目录
└── vendor         :glide下载的三方代码放置在这个目录，不用进行版本管理
```

* Makefile的模板如下：


```makefile
PWD := $(shell pwd)
GO := go
GLIDE := glide
GOCODE := gocode
TARGET := IATOpenAPI
VENDOR := ${PWD}/vendor
GOPATH := ${PWD}/gopath
OUT := ${PWD}/bin/
OUT_TARGET := ${PWD}/bin/${TARGET}

#批量工具
all: deps build package

#生成glide.yaml文件
init:
	rm -f glide.yaml
	export GOPATH=${PWD} && ${GLIDE} init

#下载三方依赖包
deps:
	rm  -rf ${GOPATH}/src
	mkdir -p ${GOPATH}/src
	export GOPATH=${PWD} && ${GLIDE} install
	ln -s ${VENDOR}/* ${GOPATH}/src/

#构建
build:
	export GOPATH=${PWD}:${GOPATH} && ${GO} build -o ${OUT_TARGET} ${PWD}/src/main.go

#清理
clean:
	rm -fr ${OUT}/*

#打包
package:
	cd ${OUT} && tar cvzf mock.tar.gz ${TARGET} config.yaml

#gocode需要依赖环境变量$GOPATH来选中pkg，因此通过使用脚本来启动gocode
gocode:
	${GOCODE} close
	GOPATH=${PWD} ${GOCODE} -s &

```

* glide支持三方包管理，但国内经常访问不了golang.org等网站，需要使用[镜像或代理](https://chenchuanyin.github.io/2017/11/07/%E4%BF%AE%E5%A4%8DGO%E5%8C%85%E7%AE%A1%E7%90%86%E5%B7%A5%E5%85%B7GLIDE%E4%B8%8D%E8%83%BD%E8%AE%BF%E9%97%AEgolang.org%E7%9A%84%E6%9B%BF%E4%BB%A3%E6%96%B9%E6%A1%88/)的方式访问。

* emacs配置go编码环境
我是emacs重度使用者，coding的时候会优先选择emacs。 经过一段时间的探索，常规项目可以通过emacs下编写go代码，自动补全。
1. 自动补全配置：spacemacs打开两个layer:go,autocomplete；gocode使用到了$GOPATH，需要根据项目目录来配置$GOPATH，配置启动方式我放在makefile脚本里。
2. 代码跳转配置：go-guru使用到了环境变量$GOPATH，因此根据项目目录来配置$GOPATH，配置方式可以通过打开emacs后`M-x setenv <RET> GOPATH <RET> GO_DIRS`来设置。
