---
title: "cpp目录结构及工具相关的一些工程经验总结"
date: 2018年 1月15日 星期一 11时41分42秒 CST
tags: [cpp]
author: chenchuanyin
category: 学习
---

> 在开发Linux环境下cpp组件时需要版本管理及组件管理，自己形成了一套模式框架，对于常规项目开发可以方便套用。

### 工具
* 编辑器：使用emacs，配置文件使用spacemacs
* 自动补全：使用spacemacs的两个layer：`auto-complete`、`c/c++`。

```elisp
(auto-completion :variables
                 auto-completion-enable-sort-by-usage t)
```

```elisp
(c-c++ :variables
       c-c++-default-mode-for-headers 'c++-mode
       c-c++-enable-clang-support t
       c-c++-enable-clang-format-on-save t
       c-c++-enable-google-newline t
       c-c++-enable-google-style t)
```

同时，针对项目来配置.clang_complete文件。

```text
-Wall
-std=c++11
-Wc++-compat
-I.
-Ithird_party/googletest/include
-Ithird_party/benchmark/include
-Ithird_party/googletest
-Ithird_party/abseil-cpp
```

* 自动跳转工具：使用ctags，配置spacemacs的`ctags` layer


```elisp
     (gtags :disabled-for go clojure emacs-lisp javascript latex python shell-scripts)
```

* 代码格式化工具：使用clang-format,配置.clang-format文件
* 调试工具：GDB
* 项目代码编译管理工具：cmake
* 脚本工具：makefile

### 目录结构


```text
.
├── CMakeLists.txt         :cmake工程文件
├── Makefile               :构建管理文件
├── .clang_complete        :自动补全依赖文件
├── doc                    :文档目录
    ├── README.md
├── out                    :构建编译编译目录
├── src                    :项目代码目录
│   ├── CMakeLists.txt
└── third_party            :第三方依赖目录
    ├── abseil-cpp
    ├── benchmark
    ├── cctz
    ├── gflags
    ├── glog
    └── googletest
```

### 常用的第三方库
  * [gflags](https://github.com/gflags/gflags)，命令行flag设置，支持cmake
  * [googletest](https://github.com/google/googletest)，单元测试，支持cmake
  * [glog](https://github.com/google/glog)，日志打印，支持cmake
  * [benchmark](https://github.com/google/benchmark)，函数性能测试工具，支持cmake
  * [abseil-cpp](https://github.com/abseil/abseil-cpp)，common库，支持cmake
