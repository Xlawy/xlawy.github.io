---
title: 0. 最长上升子序列模板
date: 2025-03-25 02:47 +0800
categories: [代码提高课笔记, 最长上升子序列]
tags: [算法]
description: 最长上升子序列模板题
---


https://www.acwing.com/problem/content/897/

# 题目背景

![image.png|500](https://raw.githubusercontent.com/Xlawy/ImageHosting/main/img/202503242124477.png)

# 思路

![image.png](https://raw.githubusercontent.com/Xlawy/ImageHosting/main/img/202503242126821.png)


# 代码

```cpp
#include <iostream>
#include <bitset>
#include <algorithm>
#include <queue>

using namespace std;

#define ll long long

ll gcd(ll a, ll b){return b == 0 ? a : gcd(b, a % b);}
ll lcm(ll a, ll b){return a / gcd(a, b) * b;}

const int N = 1e3 + 10;

int n;
int num[N];
int dp[N];


int main(void)
{
    ios::sync_with_stdio(false); cin.tie(0); cout.tie(0);

    cin >> n;
    for(int i = 1; i <= n; i ++)
    {
        cin >> num[i];
    }

    for(int i = 1; i <= n; i ++) dp[i] = 1;

    int temp = 1;

    for(int i = 2; i <= n; i ++)
        for(int j = 1; j < i; j ++)             
           if(num[j] < num[i]) dp[i] = max(dp[i], dp[j] + 1);

    int ans = 0;
    for(int i = 1; i <= n; i ++) ans = max(ans, dp[i]);

    cout << ans << endl;

    return 0;
}
```
