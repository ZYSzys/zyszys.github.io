---
layout: post
category: Template
title: KMP字符串匹配
---

## kmp算法模板

## 代码：
```c++
#include <cstdio>
#include <cstring>
#include <algorithm>
using namespace std;
const int N = 1010;
int nex[N];
void Getnex(char *p)//求得模式串的nex数组
{
    int lp = strlen(p);
    memset(nex, 0, sizeof(nex));
    nex[0] = -1;
    int j = 0, k = -1;
    while(j < lp - 1)
    {
        if(k == -1 || p[j] == p[k])
        {
            nex[++j] = ++k;
        }
        else
        {
            k = nex[k];
        }
    }
}
int KmpSearch(char *s, char *p)//进行字符串匹配
{
    int ls = strlen(s);
    int lp = strlen(p);
    int i = 0, j = 0;
    while(i < ls && j < lp)
    {
        if(j == -1 || s[i] == p[j])
        {
            i++, j++;
        }
        else
        {
            j = nex[j];
        }
    }
    if(j == lp)
    {
        return i - j;//匹配成功返回模式串第一次在文本串中出现的位置，否则返回-1
    }
    return -1;
}
int main()
{
    char p[10] = "abab";
    char s[10] = "abacababc";
    Getnex(p);
    printf("%d\n", KmpSearch(s, p));
    return 0;
}
```


