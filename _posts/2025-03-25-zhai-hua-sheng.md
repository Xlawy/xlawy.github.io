---
title: 摘花生
date: 2025-03-25 02:47 +0800
categories: [代码提高课笔记, 最长上升子序列]
tags: [算法]
description: 123
---

https://www.acwing.com/problem/content/1017/


# 思路：

按照DP分析方法来进行分析：

状态表示：
- 集合：表示从`dp[1][1]`到`dp[i][j]`的所有路径的集合
- 属性：表示从`dp[1][1]`到`dp[i][j]`的花生数量最大值

状态计算：

- 状态计算一个很重要的划分依据是看最后一个状态是如何获得的，本题中很显然最后一个状态有两种方式来达到：
	- 从上面向下走，走到`[i][j]`
	- 从左右向右走，走到`[i][j]`
- 所以本题很显然，状态转移方程如下所示

$$
dp[i][j] = max\{dp[i-1][j], dp[i][j-1],\} + weight[i][j]
$$


# 常规代码

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

int T;
int row, col;
int num[N][N];
int dp[N][N];


int main(void)
{
    ios::sync_with_stdio(false); cin.tie(0); cout.tie(0);

    cin >> T;
    while(T --)
    {
        cin >> row >> col;
        for(int i = 1; i <= row; i ++)
        {
            for(int j = 1; j <= col; j ++)
            {
                cin >> num[i][j];
            }
        }


        for(int i = 1; i <= row; i ++)
        {
            for(int j = 1; j <= col; j ++)
            {
                dp[i][j] = max(dp[i-1][j], dp[i][j-1]) + num[i][j];
            }
        }

        cout << dp[row][col] << endl;;

    }
    



    return 0;
}
```

# 优化

这里可以进行的优化主要就是滚动数组，可以优化一些空间复杂度，因为每次dp都是上一层或者同一层，可以优化为：

```cpp
        for(int i = 1; i <= row; i ++)
        {
            for(int j = 1; j <= col; j ++)
            {
                dp[j] = max([j], dp[j-1]) + num[i][j];
            }
        }
```