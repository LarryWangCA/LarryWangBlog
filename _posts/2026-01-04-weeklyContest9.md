---
layout: post
title: "Leetcode biweekly contest 173"
date: 2026-01-04 10:00:00 -0400
categories: 周赛
---

## Leetcode 3795. Minimum Subarray Length With Distinct Sum At Least K(滑动窗口， 反复练习)
暴力解法是for循环嵌套，判断每一个subarray是否符合要求，会超时。  
本题是否distinct使用Unordered_map进行判断即可，只有元素第一次出现时才更新K的值。
元素在窗口里 出现 ≥1 次 → 只算一次 x；在窗口里 出现 0 次 → 不算 x。  
模板级记忆（非常重要）
以后看到题目里有：  
	•	最短 / 最小  
	•	连续子数组  
	•	至少 / 不小于 / ≥ / 覆盖  
👉 第一反应就是：  
```
for (j = 0; j < n; j++) {
    扩张右边界;
    while (窗口满足条件) {
        更新答案;
        收缩左边界;
    }
}
```
	•	✔️ i 不重置，是因为：  
	•	所有 < i 的左边界已经被证明“更差”  
	•	✔️ 滑动窗口依赖 单调性  
	•	✔️ i 和 j 都只会向右走  
	•	✔️ 每个元素最多进出窗口一次 → O(n)  

## Leetcode 3796. Find Maximum Value in a Constrained Sequence (了解思路)
因为绝对值不等式，我们可以列出两个关系式，核心思路如下：  
如果我们把每个位置的“允许的最大高度”记为 up[i]，那么：  
	•	初始：  
	•	up[0] = 0（因为 a[0]=0）  
	•	对于 restriction [idx, maxVal]：up[idx] = min(up[idx], maxVal)  
	•	其他位置：up[i] = +inf  
	•	相邻约束 abs(a[i]-a[i+1]) <= diff[i] 会推出：  
	•	a[i+1] <= a[i] + diff[i]  
	•	a[i]   <= a[i+1] + diff[i]  

也就是说，上界也必须满足：  
	•	up[i] <= up[i-1] + diff[i-1]（从左往右传）  
	•	up[i] <= up[i+1] + diff[i]（从右往左传）  

只要做两次扫描就能把所有 restriction 的影响传播到全局  




