---
layout: post
title: "Leetcode biweekly contest 170"
date: 2025-11-22 10:00:00 -0400
categories: 周赛
---

## 整数转二进制经典写法
从低到高按位求二进制然后取反（以string的形式保存，string比较容易操作，而不是直接用int）
```
string s;
while (n) {
    s += '0' + (n & 1);  // 从低位到高位取
    n >>= 1;
}
reverse(s.begin(), s.end());  // 翻转得到正常顺序
```

## 计算数字的波峰波谷
同上，int转为string会好判断很多（直接使用to_string()函数即可），直接暴力判断即可。

## 需要将组合中的某些元素取反
从1到n，和为Sum(可用n(n+1)/2快速计算出)。target为目标元素和，SumP为正元素和，SumN为需要取反元素和。
SumP + SumN = Sum;
SumP - SumN = target.
通过上述两个表达式，
SumP = (Sum+target)/2; //如果Sum+target是奇数，直接target不存在。
SumN= (Sum-target)/2; //可以用来快速计算哪些需要取反，如果<0也表示无解。




