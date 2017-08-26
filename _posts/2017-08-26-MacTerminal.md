---
layout: post
category: Tools
tags:
  - Mac
title: Mac Terminal命令行
---

# Mac Terminal 常用命令

<!--more-->

## 目录操作:
```bash
mkdir   #创建一个目录     mkdir filename
rmdir   #删除一个目录     rm filename
cd      #进入子目录       cd Desktop
pwd     #显示当前目录的路径名
ls      #显示当前目录的内容  ls -a(显示所有目录，包括隐藏目录)
```


## 文件操作:
```bash
head    #显示文件的最初几行                    head -20 filename
tail    #显示文件的最后几行                    ail -15 filename
cut     #显示文件每行中的某些域                cut -f1,7 -d: /etc/passwd
paste   #横向连接文件                         paste file1 file2
diff    #比较并显示两个文件的差异               cdiff file1 file2
sed     #非交互方式流编辑器                    ed "s/red/green/g" filename
grep    #在文件中按模式查找                    grep "^[a-zA-Z]" filename
awk     #在文件中查找并处理模式                awk '{print $1 $1}' filename
sort    #排序或归并文件                       sort -d -f -u file1
uniq    #去掉文件中的重复行                   uniq file1 file2
comm    #显示两有序文件的公共和非公共行         comm file1 file2
wc      #统计文件的字符数、词数和行数           wc filename
nl      #给文件加上行号                       nl file1 >file2
```


## 时间操作:
```bash
date    #显示系统的当前日期和时间               date
cal     #显示日历                            cal 8 1996
time    #统计程序的执行时间                    time a.out
```




