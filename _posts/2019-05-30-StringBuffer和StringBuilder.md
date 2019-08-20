---
layout: post                         
title:     StringBuffer和StringBuilder                         
subtitle:                            
date: 2019-05-30                     
author: luojiaqi                     
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true         
tags: java
---
# StringBuffer

字符串的组成原理就是通过该类实现的

StringBuffer可以对字符串内容进行增删

StringBuffer是字符缓冲区，是一个容器

很多方法与String相同



StringBuffer三个特点：

1.StringBuffer是可变长度的，数组也是容器，但长度不变。

2.StringBuffer可以操作多个数据类型，数组只能操作int类型

3.最终会通过toString方法变为字符串

## 1存储

+ `StringBuffer append()`：将指定数据作为参数添加到已有数据结尾处。

```java
StringBuffer sb = new StringBuffer();
StringBuffer sb1 = sb.append(123);
System.out.println(sb.toString());
System.out.println(sb==sb1);
```

结果：

```
123
true
```

`sb.append("abc").append(true).append(34);`：方法调用链，一连串调用，方法返回的是本类对象，还能继续调用本类方法

+ `StringBuffer insert(index,数据)`：将数据插入到指定index处

```java
StringBuffer sb = new StringBuffer("abcde");
System.out.println(sb.insert(3,4));
```

结果:

```
abc4de
```



## 2删除

`StringBuffer delete(start,end)`：删除缓冲区中的数据，包含start，不包含end，start必须小于等于end

```java
StringBuffer sb1 = new StringBuffer("abcde");
StringBuffer sb2 = new StringBuffer("abcde");
StringBuffer sb3 = new StringBuffer("abcde");
System.out.println(sb1.delete(2,4));
System.out.println(sb2.delete(2,2));
System.out.println(sb3.delete(2,1));
```

结果：

```
abe
abcde
Exception in thread "main" java.lang.StringIndexOutOfBoundsException: start 2, end 1, length 5
```

`StringBuffer deleteCharAt(index)`：删除指定位置处的字符

```java
StringBuffer sb1 = new StringBuffer("abcde");
System.out.println(sb1.deleteCharAt(2));
```

结果：

```
abde
```



## 3获取

`char charAt(int index)`

`int indexOf(String str))`

`int length()`

`String subString(int start,int end)`注意，返回值是String而不是StringBuffer



## 4修改

`StringBuffer replace(start,end,string)`与String类的replace参数不同

`void setCharAt(int index,char ch);`注意没有返回值

## 5反转

`StringBuffer reverse();`



## 6将缓冲区中指定数据存储到指定字符数组中

`void getChars(int srcBegin,int srcEnd,char[] dst,int dstBegin)`

```java
StringBuffer sb = new StringBuffer("abcde");
char[] s = new char[4];
sb.getChars(1,4,s,1);//将sb中的1~3字符存储到字符数组s中，从下标1开始存放
for(int i=0;i<s.length;i++)
{
System.out.println("char["+i+"]="+char[i]);
}
```

```
s[0]= 
s[1]=b
s[2]=c
s[3]=d
```

# StringBuilder

StringBuffer线程同步，StringBuilder线程不同步。

![img](http://img.mukewang.com/53a7d34300011c6005970125.jpg)

# 升级三个要素：

1.提高效率

2.简化书写

3.提高安全性