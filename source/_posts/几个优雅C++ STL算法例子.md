---
title: "几个优雅的C++ STL算法代码"
date: 2018年 4月 4日 星期三 14时44分58秒 CST
tags: [cpp]
author: chenchuanyin
category: 学习
---

> 几个使用C++11的算法例子，收藏下。

## 插入排序(Insertion Sort)
代码：
```cpp
template <class FwdIt> void insertSort(FwdIt first, FwdIt last) {
  for (auto i = first; i != last; ++i)
    std::rotate(std::upper_bound(first, i, *i), i, std::next(i));
}
```

## 快速排序(Quick Sort)
代码：
```cpp
template <class FwdIt, class Compare = std::less<typename FwdIt::value_type>>
void quickSort(FwdIt first, FwdIt last, Compare cmp = Compare{}) {
  auto const N = std::distance(first, last);
  if (N <= 1)
    return;
  auto const pivot = std::next(first, N / 2);
  std::nth_element(first, pivot, last, cmp);
  quickSort(first, pivot, cmp);
  quickSort(pivot, last, cmp);
}
```
