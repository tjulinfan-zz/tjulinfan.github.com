---
layout: post
title: "[LeetCode] Single Number"
date: 2014-06-02 15:01:26 +0800
comments: true
categories: 面试题
---
### [[LeetCode] Single Number](https://oj.leetcode.com/problems/single-number/)

#### 题意

在一组数中除了一个数以外（这个数只出现了一次），其他数都出现了两次，请在线性时间内找出这个数。

#### 解法

利用异或运算的性质 a xor a = 0，求出这些数的异或和便是那个只出现了一次的数，时间复杂度：O(n)

#### 代码

[见GitHub](https://github.com/tjulinfan/LeetCode/blob/master/Single%20Number.cpp)
