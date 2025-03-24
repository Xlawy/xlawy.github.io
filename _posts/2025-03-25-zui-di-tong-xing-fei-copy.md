---
title: 1018-最低通行费（线性DP）
date: 2025-03-25 02:47 +0800
categories: [代码提高课笔记]
tags: [算法]
description: 
---

https://www.acwing.com/problem/content/1020/

# 思路：

按照DP分析方法来进行分析：

状态表示：
- 集合：表示从`dp[1][1]`到`dp[i][j]`的所有路径的集合
- 属性：表示从`dp[1][1]`到`dp[i][j]`的开销的最小值

状态计算：

- 状态计算一个很重要的划分依据是看最后一个状态是如何获得的，本题中很显然最后一个状态有两种方式来达到：
	- 从上面向下走，走到`[i][j]`
	- 从左右向右走，走到`[i][j]`
- 所以本题很显然，状态转移方程如下所示

$$
dp[i][j] = min\{dp[i-1][j], dp[i][j-1],\} + weight[i][j]
$$

和摘花生不同的地方就是这里dp需要初始化一下，因为是求最小值

# 基本代码

```cpp
#include <iostream>
#include <bitset>
#include <algorithm>
#include <queue>

using namespace std;

#define ll long long

ll gcd(ll a, ll b){return b == 0 ? a : gcd(b, a % b);}
ll lcm(ll a, ll b){return a / gcd(a, b) * b;}

const int N = 1e2 + 10;

int n;
int w[N][N];
int dp[N][N];


int main(void)
{
    ios::sync_with_stdio(false); cin.tie(0); cout.tie(0);

    cin >> n;
    for(int i = 1; i <= n; i ++)
    {
        for(int j = 1; j <= n; j ++)
        {
            cin >> w[i][j];
        }
    }

    for(int i = 0; i <= n; i ++)
    {
        dp[0][i] = 0x3f3f3f3f;
    }
    for(int i = 0; i <= n; i ++)
    {
        dp[i][0] = 0x3f3f3f3f;
    }
    dp[0][1] = 0;
    dp[1][0] = 0;



    for(int i = 1; i <= n; i ++)
    {
        for(int j = 1; j <= n ; j ++)
        {
            dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + w[i][j];
        }
    }

    cout << dp[n][n] << endl;



    return 0;
}
```

# 优化

这题的优化也和摘花生一样，可以用滚动数组的思想优化成一维数组

```cpp
#include <iostream>
#include <bitset>
#include <algorithm>
#include <queue>

using namespace std;

#define ll long long

ll gcd(ll a, ll b){return b == 0 ? a : gcd(b, a % b);}
ll lcm(ll a, ll b){return a / gcd(a, b) * b;}

const int N = 1e2 + 10;

int n;
int w[N][N];
int dp[N];


int main(void)
{
    ios::sync_with_stdio(false); cin.tie(0); cout.tie(0);

    cin >> n;
    for(int i = 1; i <= n; i ++)
    {
        for(int j = 1; j <= n; j ++)
        {
            cin >> w[i][j];
        }
    }

    dp[0] = 0x3f3f3f3f;
    dp[1] = w[1][1];
    for(int i = 2; i <= n; i ++)
    {
        dp[i] = dp[i - 1] + w[1][i];
    }


    for(int i = 2; i <= n; i ++)
    {
        for(int j = 1; j <= n ; j ++)
        {
            dp[j] = min(dp[j], dp[j-1]) + w[i][j];
            // cout << dp[j] << " ";
        }
        // cout << endl;
    }

    cout << dp[n] << endl;



    return 0;
}
```

