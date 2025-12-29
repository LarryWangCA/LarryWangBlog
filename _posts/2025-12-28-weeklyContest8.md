---
layout: post
title: "Leetcode weekly contest 482"
date: 2025-12-28 10:00:00 -0400
categories: 周赛
---

## Leetcode 3788. Maximum Score of a Split
没啥难度，注意用long long类型，Long long的max和min是LLONG_MAX和LLONG_MIN.  
再次注意判断是==,赋值是=.  

## Leetcode 3789. Minimum Cost to Acquire Required Items （了解思路即可）
贪心思路：规则 1（最重要）  
当你同时缺 type1 和 type2 时：  
	•	比较  
costBoth vs cost1 + cost2  
	•	谁便宜用谁  

规则 2  
当只剩一边缺时：  
	•	你每补 1 个单位  
	•	比较  
costBoth vs cost单边  
	•	谁便宜用谁  

## Leetcode 3790. Smallest All-Ones Multiple (了解思路即可)
判断一个数能否整除k，我们是通过余数是否为0判断的。  
Mathematically（数本身变大的话，商也同步变大）:  
new_number = old_number × 10 + 1  
So the new remainder becomes:  
new_rem = (old_rem × 10 + 1) % k  
我们只要判断最多k次即可，如果超出了k次，结果就循环了，说明永远无法被整除。  
