---
layout: post
tags:
  - STL
title: upper_bound和lower_bound
category: C++
---

## m.lower_bound(k): 
返回一个迭代器，指向键不小于k的第一个元素。如果所有元素都小于k，则返回最后一个元素之后的位置，且该位置是越界的！！~

## m.upper_bound(k):
返回一个迭代器，指向键大于k的第一个元素。如果所有元素都小于或等于k，则返回最后一个元素之后的位置，且该位置是越界的！！~

## m.equal_range(k): 
返回一个迭代器的pair对象，它的first成员等价于m.lower_bound(k)，而second成员则等价于m.upper_bound(k)

#### 注意: 都是在前闭后开区间进行查找的！


<!--more-->


## 示例:
```c++
#include <cstdio>
#include <set>
#include <algorithm>
using namespace std;
int main()
{
    int a[6] = {1, 4, 4, 5, 7, 9};
    multiset<int>s (a, a+6);
    typedef multiset<int>::iterator iter;
    iter it;
    for(it = s.begin(); it != s.end(); it++)
    {
        printf("%d\t", *it);
    }
    printf("\n");
    int k = 7;
    it = s.lower_bound(k);
    printf("%d\n", *it);
    //指向不小于k的第一个元素, 即k本身7
    it = s.upper_bound(k);
    printf("%d\n", *it);
    //指向键大于k的第一个元素, 即k下一个元素9
    pair<iter, iter> p = s.equal_range(5); 
    printf("%d %d\n", *p.first, *p.second);
    //first相当于s.lower_bound(5)--5, second相当于s.upper_bound(5)--7
    return 0;
}
```
