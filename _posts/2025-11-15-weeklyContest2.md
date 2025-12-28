---
layout: post
title: "Leetcode weekly contest 476"
date: 2025-11-15 10:00:00 -0400
categories: 周赛
---

## hasZero
在循环中不要莫名其妙突然开始用n进行处理！循环体变量是i。  
判断一个数中是否有0，经典取余和除法相结合。
```
    bool hasZero(long long n) {
        while (n > 0) {
            if (n % 10 == 0)   // 当前位是 0
                return true;
            n /= 10;            // 去掉最低位
        }
        return false;
    }
```
数位dp跳过，没练过，面试出现概率太低。

## full combination
求数组的全组合，而不是特定个数k的组合数，直接将k的终止条件取消，每一个都保存。
```
    vector<int> path;
    vector<vector<int>> res;

    void backtracking(const vector<int>& nums, int startIndex) {
        for (int i = startIndex; i < (int)nums.size(); i++) { // 注意 <= 会越界！
            path.push_back(nums[i]);
            res.push_back(path);
            backtracking(nums, i + 1);
            path.pop_back();
        }
    }
```





