---
layout: post
title: "Leetcode weekly contest 480"
date: 2025-12-06 10:00:00 -0400
categories: 周赛
---

## Leetcode 3775 Reverse Words With Same Vowel Count
正确的「拆分 string(单词之间有一个空格做区分） → vector<string>」写法（推荐）
注意else一定要有，否则下一个单词会多一个空格。   
```
vector<string> splitWords(string s) {
    vector<string> res;
    string cur;

    for (char c : s) {
        if (c == ' ') {
            res.push_back(cur);
            cur.clear();
        } else {
            cur.push_back(c);
        }
    }
    res.push_back(cur); // 最后一个单词
    return res;
}

```
res[0][i]:可以用于访问第一个单词的各个字母。

## Leetcode 3776 Minimum Moves to Balance Circular Array
circular array一圈圈寻找左右邻居（取余的使用！）
```
        // 从距离 1 开始，一圈一圈往外
        for (int distance = 1; distance < numPeople && debtAmount > 0; distance++) {

            int leftIndex  = (debtorIndex - distance + numPeople) % numPeople;
            int rightIndex = (debtorIndex + distance) % numPeople;
```

对于以下语句：
```
balance[leftIndex]  // int
debtAmount          // long long
long long takeFromLeft = min<long long>(balance[leftIndex], debtAmount);
```
<> 不是类型转换，是“模板参数”!
std::min要求两个参数是同一类型，不能直接使用min(balance[leftIndex], debtAmount)    
也可以用以下显式转换：
```
long long take = min((long long)balance[leftIndex], debtAmount);
```





