---
layout: post
title: 树状数组
category: Template
---

# 树状数组模板


```c++
#include <cstdio>
#include <cstring>
const int N = 50010;
int a[N], c[N];
int n;
int Lowbit(int x)
{
    return x & (-x);
}
void Update(int i, int x)
{
    while(i <= n)
    {
        c[i] += x;
        i += Lowbit(i);
    }
}
int Sum(int x)
{
    int sum = 0;
    while(x > 0)
    {
        sum += c[x];
        x -= Lowbit(x);
    }
    return sum;
}
int main()
{
    int t, cas = 0;
    scanf("%d", &t);
    while(t--)
    {
        scanf("%d", &n);
        memset(a, 0, sizeof(a));
        memset(c, 0, sizeof(c));
        for(int i = 1; i <= n; i++)
        {
            scanf("%d", &a[i]);
            Update(i, a[i]);
        }
        printf("Case %d:\n", ++cas);
        char s[10];
        while(~scanf("%s", s) && s[0] != 'E')
        {
            int i, j;
            scanf("%d%d", &i, &j);
            if(s[0] == 'Q')
            {
                printf("%d\n", Sum(j)-Sum(i-1));
            }
            else if(s[0] == 'A')
            {
                a[i] += j;
                Update(i, j);
            }
            else
            {
                a[i] -= j;
                Update(i, -j);
            }
        }
    }
    return 0;
}
```





