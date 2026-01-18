---
layout: post
title: "Leetcode biweekly contest 174"
date: 2026-01-18 10:00:00 -0400
categories: 周赛
---

## Leetcode3809. Best Reachable Tower
题目本身简单模拟即可，
注意字典序：if (xaxis < res[0] || (xaxis == res[0] && yaxis < res[1]))
这和if (xaxis <= res[0] && yaxis < res[1])不一样！！！

## Leetcode 3810. Minimum Operations to Reach Target Array(了解思路)
查找vector中不同元素的个数，用哈希表类方法比较好O(N),优于排序法O(NlogN)
```
#include <unordered_set>
int distinctCount(const vector<int>& a) {
    unordered_set<int> s;
    s.reserve(a.size());          // 可选：减少rehash（减少中途反复扩容）
    for (int x : a) s.insert(x);
    return (int)s.size();
}
```
 unordered_set 只有 key（元素本身），没有 value.
