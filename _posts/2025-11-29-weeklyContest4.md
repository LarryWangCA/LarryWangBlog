---
layout: post
title: "Leetcode weekly contest 478"
date: 2025-11-29 10:00:00 -0400
categories: 周赛
---

# C++ Tips
c++中：iterator - iterator  ==  一个整数（距离）

## Leetcode 3759 Count Elements With at Least K Greater Values（反复练习）
数组排序后，同upper_bound()函数求出第一个比当前元素大的元素的位置，之后右侧所有元素个数便可计算。  
具体用法：  
头文件: algorithm。  
函数签名:  
iterator upper_bound(iterator first, iterator last, const T& value);
first: 搜索范围的起始迭代器。  
last: 搜索范围的结束迭代器。  
value: 要查找的值。  
iterator: 返回的迭代器类型，取决于容器。  
作用: 返回一个迭代器，指向 [first, last) 范围内第一个大于 value 的元素。   


## Leetcode 3760 Maximum Substrings With Distinct Start（反复练习）
因为需要每个子串的开头字母不同，我们遍历一次统计每个字母最后一次出现的位置。  
第二次遍历，当我们走到一个字符的最后一次出现时，说明：  
它之前所有出现都已经“处理完毕”；
后面再也不会出现这个字符了；
现在安全把它用作某个子串的开头！
此时统计结果即可。

## Leetcode 3761 Minimum Absolute Distance Between Mirror Pairs(反复练习)
经典整数反转的方法(120会变成21,开头的0省略)：
```
    int reverseNum(int x) {
        if (x == 0) return 0;
        int res = 0;
        while (x > 0) {
            res = res * 10 + x % 10;
            x /= 10;
        }
        return res;
    }
```
核心思路是保存当前遍历元素的反转值和下标位置到map：lastPos中，之后进行遍历匹配。  
每次循环 j 时，做两件事：  
	1.	先用当前值 nums[j] 去“收割前面的信息”  
	•	如果之前有人 i 的反转值等于 nums[j]，就构成 mirror pair  
	•	具体就是查 lastPos[nums[j]] 有没有  
	2.	再把自己作为“未来的 i”存进去  
	•	计算 rev = reverseNum(nums[j])  
	•	记下：以后如果遇到值等于 rev 的位置 k，就可以和当前 j 配对。  
	•	用 lastPos[rev] = j 更新为“最近的 i”。  
整个过程只扫一遍数组，哈希查找是 O(1) 均摊，总复杂度 O(n)。  






