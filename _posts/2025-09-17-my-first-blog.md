---
layout: post
title: "代码训练营Day1-数组01"
date: 2025-09-17 12:00:00 -0400
categories: 随笔
---

## Leetcode704二分查找
二分查找，选择左闭右闭更符合我的直觉，即下标left = 0, right = array.size()-1;<br/>  
此时left==right makes sense<br/>
mid=left+(right-left)/2而不是mid=(left+right)/2,这种写法的好处是防止left+right过大溢出（超过 int类型的范围）

## Leetcode27移除元素
暴力解法为两层for循环嵌套，第一层为遍历各个元素，第二层当找到目标元素后，将目标元素之后的所有元素粘贴过来 o(n^2)<br>
**双指针法**，快指针用于判断，慢指针用于更新数组

## Leetcode977有序数组的平方
我自己的想法（暴力解法）：各个元素平方之后重新排序 O(nlogn):排序的复杂度
**双指针法** 有序数组，平方后的值要么依旧最小，要么从最小变成最大<br/>
A指针在最左边，B指针在最右边，从右向左更新（从大到小）<br/>
需要新开一个vector用户存答案，不能直接改变原有数组的元素大小<br/>
此方法为O(n)
