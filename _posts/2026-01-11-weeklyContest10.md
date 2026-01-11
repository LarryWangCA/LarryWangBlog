---
layout: post
title: "Leetcode biweekly contest 173"
date: 2026-01-04 10:00:00 -0400
categories: 周赛
---

# C++ Tips
在 C++ 里，a % b 的结果 和 a（被除数）同号  


## Leetcode 3804. Number of Centered Subarrays
for魂环暴力列举每个subarray时，外层为起点，内层为从起点到终点，比较方便。
```
        for (int i = 0; i < length; ++i) {
            
            for (int j = i; j < length; ++j)
```

## 3806. Maximum Bitwise AND After Increment Operations(目前只了解部分思路)
假设（只看 4 位方便）：
	•	targetMask = 1011
	•	value      = 1001

那缺哪些位？target 要求 bit1=1，但 value 的 bit1=0，所以缺 0010。

算一遍：
	•	~value = ~1001 = 0110（4位视角）
	•	targetMask & ~value = 1011 & 0110 = 0010 ✅

所以 missingBits = 0010，表示“缺 bit1”。
