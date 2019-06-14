---
layout: post                          
title: 链表中倒数第k个节点                              
subtitle:                             
date: 2019-06-04                      
author: luojiaqi                      
header-img: img/post-bg-re-vs-ng2.jpg 
catalog: true                         
tags:                                 
	剑指offer
---

牛客网OJ [链表中倒数第k个节点](![1559652094983](<https://www.nowcoder.com/practice/529d3ae5a407492994ad2a246518148a?tpId=13&tqId=11167&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking>))

# 题目描述

输入一个链表，输出该链表中倒数第k个结点。

# 思路

假设链表有n个节点，那么倒数第k个节点就是从头节点开始的第n-k+1个节点。

如果能够得到链表长度n，从头开始走n-k+1步就能找到目标节点。

如何得到n？从头到尾遍历，每经过一个节点计数+1.

定义两个指针，让第一个指针先走k-1步，第二个指针不动。从第k步开始，两个指针一起走。这样两个指针的距离就一直保持在k-1，当第一个结点到达链表尾节点时，第二个节点正好走到倒数第个节点。

**注意特殊输入：**

+ 链表为空
+ 链表长度n<k
+ k=0

# 代码：

```java
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
		if (head==null||k==0)//链表为空或k=0
            return null;
        ListNode p1,p2;
        p1 = p2 = head;
        for(int i=1;i<k;i++){//p1往前走k-1步
            if(p1.next!=null)
                p1 = p1.next;
            else
                return null;//如果还没走到k-1步就走到头了，说明k>n，返回null
        }
        while(p1.next!=null){//两个指针同时走
            p1 = p1.next;
            p2 = p2.next;
        }
        return p2;
    }
}
```

```java
//简洁版
public class Solution {
	public ListNode FindKthToTail(ListNode head,int k) {
        ListNode p, q;
        p = q = head;
        int i = 0;
        for (; p != null; i++) {
            if (i >= k)
                q = q.next;
            p = p.next;
        }
        return i < k ? null : q;
    }
}
```

