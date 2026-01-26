---
layout: post
title: "Leetcode weekly contest 486"
date: 2026-01-25 10:00:00 -0400
categories: 周赛
---

## Leetcode 3819. Rotate Non Negative Elements（了解思路）
纯模拟题，学习将旧数组插入新数组的方法：  
新建一个数组，将原数组分两次插入即可。
```
        k %= positions.size();
        vector<int> rotated;
        for (int i = k; i < positions.size(); i++)
            rotated.push_back(values[i]);
        for (int i = 0; i < k; i++){
            rotated.push_back(values[i]);
        }
```


## Leetcode 3820. Pythagorean Distance Nodes in a Tree（反复练习，类似于bfs模版题）
题意本身等价于x,y,z三个点到其余所有点的最短距离（因为是无向图），用bfs即可。  
复习之前的bfs内容，注意边的关系用领接表比较合适。  
```
        // 1) 建图：邻接表
        vector<vector<int>> adj(n);
        for (auto &e : edges) {
            int u = e[0], v = e[1];
            adj[u].push_back(v);
            adj[v].push_back(u);
        }

```
注意同样需要去重，取决于该点的距离有没有更新过。  

## Leetcode 3821. Find Nth Smallest Integer With K One Bits (了解思路)
把所有满足 popcount = k 的数按从小到大排序。  
从高位到低位逐位决定答案 res 的每一位是 0 还是 1。  

关键：在决定第 i 位（2^i）时，先假设它为 0：  
	•	若第 i 位为 0，剩下低位可用位置是 i 个（0..i-1），还需要放 k 个 1，可形成的合法数数量为  
c = C(i, k) （基础组合数类型dp）
```
    long long comb[51][51] = {0};
    for (int i = 0; i <= 50; i++) {
        comb[i][0] = 1;
        for (int j = 1; j <= i; j++) {
            comb[i][j] = comb[i - 1][j - 1] + comb[i - 1][j];
        }
    }
```
找出每一位在每种情况下的组合数之后：  
	•	若 n <= c：第 n 个仍在这一段（bit i = 0），保持 0  
	•	若 n > c：说明要跳过这 c 个（bit i = 0 的整段），答案第 i 位必须为 1，更新：  
	•	res |= (1LL << i)  
	•	n -= c  
	•	k -= 1（用掉了一个 1）  
	•	若 k == 0 提前结束  
