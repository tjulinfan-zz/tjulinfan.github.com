---
layout: post
title: "Codeforces Beta Round #5 解题报告"
date: 2014-04-29 12:25:09 +0800
comments: true
categories: ACM-ICPC, CF
---
### [CF5A Chat Servers Outgoing Traffic](http://codeforces.com/contest/5/problem/A)

#### 题目大意

三种操作：添加一个人，删除某个人，向名单中所有人发送一条消息。问所有操作之后发送的消息总长度。

#### 解法

直接用 map 保存这个人名，然后要发送消息时统计 _map 中人数 * 消息长度_ 加到答案中。

感觉这题很黄很暴力。。。

#### 代码

[见GitHub](https://github.com/tjulinfan/Codeforces/blob/master/Codeforces%20Beta%20Round%20%235/CF5A.cpp)


### [CF5B Center Alignment](http://codeforces.com/contest/5/problem/B)

#### 题目大意

输入一些字符串，将这些字符串跟其中最长的字符串居中对齐，当不能完全居中时，第一次此种情况左边多一格，下一次这种情况右边多一格，以此类推输出。

#### 解法

很水，简单除一下然后加个标识变量即可。

#### 代码

[见GitHub](https://github.com/tjulinfan/Codeforces/blob/master/Codeforces%20Beta%20Round%20%235/CF5B.cpp)

### [CF5C Longest Regular Bracket Sequence](http://codeforces.com/contest/5/problem/C)

#### 题目大意

一个只包含左括号右括号的序列，求其中合法嵌套的最长子序列以及最长子序列个数。

#### 解法

根据括号匹配的性质我们可以用栈存储当前位置之前的所有左括号，而用len[i]表示当前位置（右括号）向前的合法序列长度。很显然：假如当前位置i是左括号则将其入栈，否则计算len[i]，如果栈不为空则弹栈顶x，**_len[i]=len[x - 1] + i - x + 1_**，栈为空则len[i]为0。最后再遍历一遍统计答案。

#### 代码

[见GitHub](https://github.com/tjulinfan/Codeforces/blob/master/Codeforces%20Beta%20Round%20%235/CF5C.cpp)

### [CF5D Follow Traffic Rules](http://codeforces.com/contest/5/problem/D)

#### 题目大意

在一条马路上（长度为l），一辆车初速度为0，加速度为a，极限速度为v，然后在离起点为d的地方限时速在w之内，问该车最少多久可以到达终点。

#### 解法

这个题基本学过高中物理的应该想起来都比较简单，但是写起来其实还是有点蛋疼的，参考了官方题解发现有两个函数还是很巧妙的。下面讲一下具体的解法吧：

两个函数：

1.dist(speed, time) <br />
初速度为speed，加速度为a的情况下可以行使的路程，很显然为 **_speed * time + a * time * time / 2_**

2.travelTime(distance, speed) <br />
在不考虑极限速度的情况下： **_speed * time + a * time * time / 2 = distance_** 这个一元二次方程可以通过求根公式直接求出非负根，求出的时间设为 **tAll** ,设 **_tMax = (v - speed) / a_** ，如果tMax>=tAll那么该函数的返回值就是 **tAll**，否则应该返回 **_tMax + (distance - dist(speed, tMax)) / v_**

<br />
>接下来就是 **O(1)** 时间内求出解：
>
>1. w >= v  
>答案就是**travelTime(l, 0)**
>
>2. w < v  
>计算 **tw = w / a, dw = dist(0, tw)**  
>  2.1 dw >= d 答案是 **travelTime(l, 0)**  
>  2.2 dw < d 答案是 **tw + travelTime((d - dw) / 2, w) * 2 + travelTime(l - d, w)**

#### 代码

[见GitHub](https://github.com/tjulinfan/Codeforces/blob/master/Codeforces%20Beta%20Round%20%235/CF5D.cpp)


### [CF5E Bindian Signalizing](http://codeforces.com/problemset/problem/5/E)

#### 题目大意

在一个环上有n个点，每个点有个高度，问有多少对点可以互相看见，互相看见是指在顺时针方向或者逆时针方向上没有其他点的高度超过这对点中的任意一个。

#### 解法

由于是一个环，我们要尽量得将其变成直线上来做——选取高度最大的点放在起始位置，后面的按顺时针或者逆时针依次放置。同时最后再放置一个高度最大的点。
  
每个点记录三个值l， r， c
  
+ l 表示向左最近的高度比该点大的位置（没有就记为-1）  
+ r 表示向右最近的高度比该点大的位置 (没有就记为n + 1)
+ c 表示从 l 到该点位置中与该点高度相同的点的个数

很显然，对于当前点来说答案应该加上：

+ 如果 l 不为-1则加上1
+ 如果 r 不为n+1则加上1
+ 如果 l 为0，r 为n则减去1（因为首尾其实是一个点）
+ 答案加上c

#### 代码

[见GitHub](https://github.com/tjulinfan/Codeforces/blob/master/Codeforces%20Beta%20Round%20%235/CF5E.cpp)

### 总结

CF很多题都是很巧妙的，感觉自己好弱啊。。。