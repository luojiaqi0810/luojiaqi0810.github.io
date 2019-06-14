---
layout: post                          
title: 和为S的两个数字                               
subtitle:                             
date: 2019-06-13                      
author: luojiaqi                      
header-img: img/post-bg-re-vs-ng2.jpg 
catalog: true                         
tags:                                 
	剑指offer                              
---

牛客网OJ [和为S的两个数字](<https://www.nowcoder.com/practice/390da4f7a00f44bea7c2f3d19491311b?tpId=13&tqId=11195&tPage=3&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking>)

# 题目描述

输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。

 输出描述:

```
对应每个测试案例，输出两个数，小的先输出。
```

# 思路

数组已经排好序，可以左右夹逼。

乘积最小：显然两数相差越大，乘积越小，所以找到的第一组就是最终结果。

有点类似于leetcode上的twoSum，只不过twoSum要求返回下标，不然也可以先排序再夹逼，可以达到O(nlogn)。

# 代码

```java
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> FindNumbersWithSum(int [] array,int sum) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        if (array == null || array.length < 2) {
            return list;
        }
        int i = 0, j = array.length-1;
        while (i < j){
            if (array[i] + array[j] == sum){
                list.add(array[i]);
                list.add(array[j]);
                return list;
            }
            else if (array[i] + array[j] > sum){
                j--;
            }
            else {
                i++;
            }             
        }
        return list;
    }
}
```

