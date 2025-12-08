---
layout: post
title: "Leetcode weekly contest 479"
date: 2025-12-06 10:00:00 -0400
categories: 周赛
---

# C++ Tips 再次复习lambda表达式和cmp的转换
```
sort(arr.begin(), arr.end(), [](auto &a, auto &b){
    if (a.first != b.first) return a.first < b.first;
    return a.second < b.second;
});
```
转换为cmp函数(注意需要使用static，或者放到class外)：
```
static bool cmp(const pair<int,int>& a, const pair<int,int>& b) {
    if (a.first != b.first) return a.first < b.first;
    return a.second < b.second;
}
```


## Leetcode 3769 Sort Integers by Binary Reflection（反复练习）
本题根据二进制反转值的大小对原数组进行排序，第一步是求二进制的反转。
求二进制的反转LC190,固定32位(注意需要先左移然后再写入数值！)：
```
    for (int i = 0; i < 32; ++i) {
        res <<= 1;          // 左移为下一位腾位置
        res |= num & 1;     // 取出 num 的最低位写入 res
        num >>= 1;          // num 右移
    }
```
e.g.   
0000 0000 0000 0000 0000 0000 0000 0110  
翻转 → 0110 0000 0000 0000 0000 0000 0000 0000  
→ 很大的数 = 1610612736  
但是本题需要忽略先导0，需要使用短翻转。
```
        while (num > 0){
            res <<= 1;
            res |= num & 1;
            num >>= 1;
        }
```
e.g. 6 = 110； 翻转 → 011 → 十进制 = 3。  
短翻转和长翻转的结果完全不同，必须区分清楚！
本题需要使用vector<pair<int,int>>,而不是map，因为不同数值的反转值有可能相同。
自定义排序后保存结果即可。

## Leetcode 3770. Largest Prime from Consecutive Prime Sum
求prime的方法：
```
    bool isPrime(int x) {
        if (x < 2) return false;
        for (long long i = 2; i * i <= x; ++i) {
            if (x % i == 0) return false;
        }
        return true;
    }
```
本题如果从2到n每个数都判断是否为prime，再累加，容易超时；判断prime和循环次数较少（根本到不了n次）。  
	•	版本一：  
	•	对 2..10^6 每个数，都试除到 √i ≈ 1000  
	•	调用次数 ≈ 10^6 次，每次最多 1000 步 → 10^9 步，危险  
	•	版本二：  
	•	x 只需要跑到大概 1000 左右（因为前面那一堆质数和已经爆到 ≥10^6 了）  
	•	while 大约 1000 步  
	•	每步判素数最多 1000 次除法 → 10^6 步，很轻松  

## Leetcode 3771. Total Score of Dungeon Runs
本题暴力解法很简单，两层for循环即可，但是会超时。  
暴力是这样：“我选一个起点 s，看它能得哪几个 j。”  
我们换个想法：“我选一个房间 j，看看有哪些起点 s 能让它得分。”  
这样是反着想，但完全等价。

房间 j 得分的条件！（掉血后 hp ≥ requirement）：
hp - (damage[s] + … + damage[j]) >= requirement[j] (重要公式)  
上述公式中伤害的计算可以使用前缀和。
（⭐当你发现题目中出现「重复计算连续东西」的时候，90% 就应该用前缀和！）

```
公式递推：
damage[s] + ... + damage[j] = pref[j+1] - pref[s];
hp - (pref[j+1] - pref[s]) ≥ requirement[j];
pref[s] ≥ requirement[j] - hp + pref[j+1];
L_j = requirement[j] - hp + pref[j+1]
```
所以，房间 j 得分 <=> 找所有满足：
pref[s] ≥ L_j （s 区间是 0..j）
之后对于每个房间j，找出符合要求的起点即可(pref是递增的因为伤害不可能为负，t0后的都会符合要求)：
```
            // 在 pref[0..j] 中找第一个 >= Lj 的下标 t0
            int t0 = lower_bound(pref.begin(), pref.begin() + (j + 1), Lj) - pref.begin();

            if (t0 <= j) {
                // s 可以取 [t0 .. j]，个数 = j - t0 + 1
                ans += (long long)(j - t0 + 1);
            }
```
lower_bound, upper_bound函数本质上是二分查找。  









