---
layout: post                          
title: 最小的k个数                               
subtitle:                             
date: 2019-06-03                      
author: luojiaqi                      
header-img: img/post-bg-re-vs-ng2.jpg 
catalog: true                         
tags:                                 
	剑指offer                              
---

牛客网OJ [最小的k个数](https://www.nowcoder.com/practice/6a296eb82cf844ca8539b57c23e6e9bf?tpId=13&tqId=11182&tPage=2&rp=2&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

# 题目描述

输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

# 思路1：最蠢的方法，排序后再输出



# 代码

```java
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
        ArrayList<Integer> res = new ArrayList<Integer>();
        if(k>input.length||k<=0)
            return res;
        for(int i=0;i<k;i++)//冒泡排序，不需要把所有的数都排序，找到k个最小的就行
        {
            for(int j=input.length-1;j>i;j--)
            {
                if(input[j-1]>input[j])
                {
                    int tmp = input[j];
                    input[j] = input[j-1];
                    input[j-1] = tmp;
                }
            }
            res.add(input[i]);
        }
        return res;
    }
}
```



