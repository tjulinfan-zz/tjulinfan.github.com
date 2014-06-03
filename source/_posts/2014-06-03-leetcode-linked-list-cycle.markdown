---
layout: post
title: "[LeetCode] Linked List Cycle"
date: 2014-06-03 21:38:16 +0800
comments: true
categories: LeetCode 面试题
---

### [[LeetCode] Linked List Cycle](https://oj.leetcode.com/problems/linked-list-cycle/)

#### 题意

判断一个单向链表中是否有环，要求利用额外的常数空间。

#### 解法

设两个指针变量一开始都指向链表的头结点，其中一个每次走一步（p1），另一个每次走两步（p2），如果两个指针再次相遇则说明有环。

个人的想法是这样的：假设p1从头结点走到环开始的地方要a步，在环内与p2相遇时走了b步，同时环的大小是k，那么显然：

[2(a + b) - a] % k ≡ b % k

那么 (a + b) % k ≡ 0
这个证明可以在O(k)的时间内出解

#### 代码

[见GitHub](https://github.com/tjulinfan/LeetCode/blob/master/Linked%20List%20Cycle.cpp)

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     ListNode *next;
	 *     ListNode(int x) : val(x), next(NULL) {}
	 * };
	 */
	class Solution {
	public:
	    bool hasCycle(ListNode *head) {
	        
	        ListNode *p1 = head, *p2 = head;
	        do {
	            if (p1 == NULL || p2 == NULL || p2 -> next == NULL) return false;
	            p1 = p1 -> next;
	            p2 = p2 -> next -> next;
	        } while (p1 != p2);
	        return true;
	    }
	};