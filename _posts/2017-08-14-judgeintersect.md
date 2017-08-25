---
layout: post
title: 判断线段相交
category: Template
---

# 计算叉积，根据快速排斥实验和跨立实验判断线段是否相交


```c++
#include <cstdio>
#include <algorithm>
using namespace std;
struct Point
{
    double x, y;
};
struct Line
{
    Point a, b;
};
double Cross(Point p0, Point p1, Point p2)// 计算叉积
{
    return ((p1.x-p0.x)*(p2.y-p0.y)-(p1.y-p0.y)*(p2.x-p0.x));
}
bool Judge(Line u, Line v)// 进行判断 是否相交
{
    if((max(u.a.x, u.b.x)>=min(v.a.x, v.b.x))&&(max(u.a.y, u.b.y)>=min(v.a.y, v.b.y))&&(max(v.a.x, v.b.x)>=min(u.a.x, u.b.x))&&(max(v.a.y, v.b.y)>=min(u.a.y, u.b.y))&&(Cross(u.a, v.a, u.b)*Cross(u.a, u.b, v.b)>=0)&&(Cross(v.a, u.a, v.b)*Cross(v.a, v.b, u.b)>=0))
    {
        return true;
    }
    return false;
}
int main()
{
    int t;
    scanf("%d", &t);
    while(t--)
    {
        Line l1, l2;
        scanf("%lf%lf%lf%lf%lf%lf%lf%lf", &l1.a.x, &l1.a.y, &l1.b.x, &l1.b.y, &l2.a.x, &l2.a.y, &l2.b.x, &l2.b.y);
        if(Judge(l1, l2))
        {
            printf("Intersected!\n");
        }
        else
        {
            printf("Not intersected!\n");
        }
    }
    return 0;
}
```
