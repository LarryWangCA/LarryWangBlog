---
layout: post
title: "Leetcode biweekly contest 172"
date: 2025-12-21 10:00:00 -0400
categories: 周赛
---

# C++ Tips
常规数组的初始化：int cnt[10001] = {0};  （写在class里是成员变量，默认为0）  
vector.erase(iterator)是按照iterator进行的，不是按照值来进行。

vector<int> a[3];与vector<vector<int>> a(3);几乎等价，唯一区别是外层是否动态（可扩展）。  
第一种写法因为外层是传统数组，不存在.begin(), .end()之类的。
个人还是倾向于第二种用法。  
注意内层排序都是sort(a[i].begin(),a[i].end());  

c++中多种条件与不用内部加括号：if (a && b && c)  

priority_queue常见复杂度：  
top()：O(1)  
push()：O(log N)  
pop()：O(log N)  
建堆（一次性）：O(N)  



## 3779. Minimum Number of Operations to Have Distinct Elements (反复练习)
nums[i]的值小于等于100000，不代表i有这么大！
本题是模拟题，统计频次常用方法如下：
```
        static const int MAXV = 10000;
        int freq[MAXV + 1] = {0};

        for (int v : nums) freq[v]++;

        int dupKinds = 0;
        for (int x = 0; x <= MAXV; x++) {
            if (freq[x] >= 2) dupKinds++;
        }
```
因为erase的时间复杂度是O(N),本题可以用startIndex从而避免使用erase。
统计出总的dupKinds并更新，同时更新具体数字的频率（当前频次为2的时候，删除后即不重复）。  
```
        int ops = 0;
        int n = (int)nums.size();
        int start = 0;

        while (start < n && dupKinds > 0) {
            ops++;
            for (int k = 0; k < 3 && start + k < n; k++) {
                int v = nums[start + k];
                if (freq[v] == 2) dupKinds--; // 2 -> 1 后不再重复
                freq[v]--;
            }
            start += 3;
        }
        return ops;
```

## 3780. Maximum Sum of Three Numbers Divisible by Three （了解思路即可）
很少会用回溯的暴力解法（太费时），本题属于贪心加纯数学理解。  
3️⃣ 枚举「合法组合」取最大值  
	•	三个 %3 == 0
	•	三个 %3 == 1
	•	三个 %3 == 2
	•	一个 %3 == 0 + 一个 %3 == 1 + 一个 %3 == 2  
4种情况取最大的。

## Leetcode 3781. Maximum Score After Binary Swaps (反复练习)
核心难点在于对题意的理解，是一道heap的好题。    
关键是：你允许的操作是把 01 -> 10，也就是 把 1 往左“冒泡”，所以：  
	•	1 可以往左穿过任意多个 0 （只要左边有0，可以一直交换，而不是只有一次！）  
	•	但 不能越过别的 1（相对顺序不变）  
	•	等价于：第 j 个 1 最终只能落在 它原来位置 pj 的左边（含 pj），即 qj <= pj  
核心在于使用最大堆（类似于k个数中选最大的），原数组遇到1（need）即表示此时至少有一个数需要被选择。  
用变量记录选择的个数（最大堆弹出的次数），如果小于need则弹出。  
```
        for (int i = 0; i < (int)s.size(); i++) {
            if (s[i] == '1') need++;
            pq.push(nums[i]);

            while (picked < need) {
                ans += pq.top();
                pq.pop();
                picked++;
            }
        }
        return ans;
    }
```




