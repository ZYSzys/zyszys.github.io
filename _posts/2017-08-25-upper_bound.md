---
layout: post
tags:
  - STL
title: upper_bound和lower_bound
category: C++
---

m.lower_bound(k): 返回一个迭代器，指向键不小于k的第一个元素

m.upper_bound(k): 返回一个迭代器，指向键大于k的第一个元素

m.equal_range(k): 返回一个迭代器的pair对象，它的first成员等价于m.lower_bound(k)，而second成员则等价于m.upper_bound(k)



示例:
```c++
#include <cstdio>
#include <set>
#include <algorithm>
using namespace std;
int main()
{
    int a[6] = {1, 6, 4, 4, 9, 5};
    sort(a, a+6);
    //一般先排序，排完序后a[6]={1, 4, 4, 5, 6, 9}
    multiset<int>s (a, a+6);
    typedef multiset<int>::iterator iter;
    printf("Start: %d\tEnd: %d\n", *s.begin(), *(--s.end()));
    it = s.lower_bound(5);
    printf("%d\n", *--it);
    iter it = s.upper_bound(4);
    printf("%d\n", *it);
    pair<iter, iter> p = s.equal_range(5); 
    printf("%d %d\n", *--p.first, *p.second);
    return 0;
}
```
