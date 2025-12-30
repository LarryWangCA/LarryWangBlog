---
layout: post
title: "Leetcode Biweekly contest 169"
date: 2025-11-08 10:00:00 -0400
categories: 周赛
---

## 前缀和
for (auto x : nums) 中的 x 是 每个元素的副本；你修改 x 不会影响 nums 里面的真实值。  

前缀和问题，常用写法,注意一般额外开辟一个空间：
```
vector<int> nums = {1, 2, 3, 4, 5};
int n = nums.size();

// 前缀和数组多开一个空间，方便计算
vector<int> prefix(n + 1, 0);

// prefix[i] 表示 nums[0..i-1] 的和
for (int i = 1; i <= n; i++) {
    prefix[i] = prefix[i - 1] + nums[i - 1];
}


// 求所有子数组的和
long long total = 0;
for (int l = 0; l < n; ++l) {
    for (int r = l; r < n; ++r) {
        int sum = prefix[r+1] - prefix[l];
        total += sum;
    }
}
```

有时候问题可以直接用for循环嵌套暴力解决， 不一定是dp或者贪心类问题。




