---
layout: post
category: ACM
tags: 思维
title: XOR Sorting
---
[hihoCoder 1509 XOR Sorting](https://hihocoder.com/problemset/problem/1509)

思维题，主要考察异或的性质。
<!--more-->
# 1509 : XOR Sorting
Time Limit:10000ms  
Case Time Limit:1000ms  
Memory Limit:256MB  
## Description
Given a sequence a[1..n], you need to calculate how many integers S satisfy the following conditions:

* (1). 0 ≤ S < 2 ^ 60

* (2). For every i in [1,n-1] , (a[i] xor S) ≤ (a[i+1] xor S)

### Input
On the first line there is only one integer n

On the second line there are n integers a[1..n]

1 ≤ n ≤ 50

0 ≤ a[i] < 260

### Output
Output one integer : the answer

### Sample Input
```
3
1 2 3
```

### Sample Output
```
288230376151711744
```

## 题意
求与a[N]数组元素的异或结果非递减的数字S的个数，S小于2的60次方

## 分析
异或：二进制的同一位数字相同则为1, 不同则为0  
**(a[i] xor S) ≤ (a[i+1] xor S)**: 将a[i]与a[i+1]转化为二进制数，从高位到低位找第一个不同数字的那一位，那么满足条件的S的那一位就是确定的
* 若(a[i]j, a[i+1]j)=(0, 1), 那么Sj=0, 其余各位随意
* 若(a[i]j, a[i+1]j)=(1, 0), 那么Sj=1, 其余各位随意

对a[N]中每对相邻元素进行判断，标记不同的那一位，最后答案就是2 ^ (随意的位数的个数)

## 代码
```c++
#include <cstdio>
#include <cstring>
#define lint unsigned long long
const int N = 60;
lint a[N];
int s1[N], s2[N];
bool f[N], flag;
void Trans(lint x, lint y)//转化为二进制数存在s1，s2数组中
{
    memset(s1, 0, sizeof(s1));
    memset(s2, 0, sizeof(s2));
    
    for(int i = 0; i < N; i++)
    {
        s1[i] = x % 2, x >>= 1;
        s2[i] = y % 2, y >>= 1;
    }
}
void Judge()//从高位到低位找到第一个不相同的数字，将该位标记，则S的第i位是确定了的
{
    for(int i = N-1; i >= 0; i--)
    {
        if(s1[i] != s2[i])
        {
            f[i] = true;
            return;
        }
    }
}
int main()
{
    int n;
    scanf("%d", &n);
    scanf("%lld", &a[0]);
    memset(f, false, sizeof(f));
    flag = false;
    for(int i = 1; i < n; i++)
    {
        scanf("%lld", &a[i]);
        Trans(a[i-1], a[i]);
        Judge();
    }
    int cnt = 0;
    for(int i = 0; i < N; i++)//计数未确定位数
    {
        if(!f[i])
            cnt++;
    }
    printf("%lld\n", (lint)1 << cnt);
    return 0;
}

```
