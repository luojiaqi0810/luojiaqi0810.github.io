---
layout: post                          
title: 为什么重写equals时必须重写hashCode方法                            
subtitle:                             
date: 2019-06-04                     
author: luojiaqi                      
header-img: img/post-bg-re-vs-ng2.jpg 
catalog: true                         
tags:                                 
    面试问题                             
---

# 为什么重写equals时必须重写hashCode方法

## 为什么要重写equals

### ==与equals

+ `==`：判断两个对象的地址是否相等，即判断两个对象是不是同一个对象。

  对于基本数据类型，`==`比较的是值；

  对于引用数据类型（类、接口、数组），`==`比较的是内存地址。

+ `equals()`:

```java
//Object类中的equals方法
public boolean equals(Object obj) {  
    return (this == obj);  
    }
```

可以看出Object类中的equals方法与`==`是等效的。

有时候我们想比较的是对象的内容而不是内存地址，比如相比较两个字符串是否相等。

```java
String s1 = new String("abc");
String s2 = new String("abc");
System.out.println(s1==s2);//false
System.out.println(s1.equals(s2);//true
```

这时就可以重写`equals()`，比如String类中就重写为判断两个字符串是否相同。

## 为什么还得重写hashCode

### hashCode()介绍

hashCode()作用是获取哈希码，是通过一个哈希函数将对象的内存地址转换为整数后返回。这个哈希码的作用是确定该对象在哈希表中的索引位置。哈希表存储的是键值对(key-value)，它的特点是：能根据“键”快速的检索出对应的“值”。这其中就利用到了哈希码！（可以快速找到所需要的对象）

### hashCode()有什么用

我们知道HashSet中的元素是不重复的，所以把对象加入HashSet时，HashSet会判断是否有重复对象。

HashSet会先计算对象的hashcode值来判断对象加入的位置，同时也会与其他已经加入的对象的hashcode值作比较，如果没有相符的hashcode，HashSet会假设对象没有重复出现。但是如果发现有相同hashcode值的对象，这时会调用equals（）方法来检查hashcode相等的对象是否真的相同。如果两者相同，HashSet就不会让其加入操作成功。如果不同的话，就会重新散列到其他位置。

#### 已经有了equals()可以比较对象是否相同，为什么还要hashCode()

一般重写后的equals()比较全面和复杂，效率就比较低，而利用hashCode()进行对比，则只要生成一个hash值进行比较就可以了，效率很高。

假设集合中现在已经有1000个元素，那么第1001个元素加入集合时，它就要调用1000次equals方法。这显然会大大降低效率。   

于是，Java采用了哈希表的原理。  这样一来，当集合要添加新的元素时，先调用这个元素的hashCode方法，就一下子能定位到它应该放置的物理位置上。 

如果这个位置上没有元素，它就可以直接存储在这个位置上，不用再进行任何比较了；

如果这个位置上已经有元素了，就调用它的equals方法与新元素进行比较，相同的话就不存，不相同就散列其它的地址。所以这里存在一个冲突解决的问题。这样一来实际调用equals方法的次数就大大降低了，几乎只需要一两次。

#### hashCode()既然效率这么高为什么还要equals()呢？

因为hashCode()并不是完全可靠，有时候不同的对象他们生成的hashcode也会一样（称为散列冲突，跟采用的哈希函数有关），所以hashCode()只能说是大部分时候可靠，并不是绝对可靠，所以我们可以得出：

- (1)equals()相等的两个对象他们的hashCode()肯定相等，也就是用equals()对比是绝对可靠的。
- (2)hashCode()相等的两个对象他们的equals()不一定相等，也就是hashCode()不是绝对可靠的。

---

**回到问题：为什么还得重写hashCode**

因为Java中的基于散列的集合（HashMap、HashSet、HashTable）都会用到hashCode()和equals()，如果一个类的实例对象要放到这类几何中，当你重写了equals()，却不重写hashCode()，会产生违反上面第(1)条规定，会导致Hash结构的集合不能正常工作。

比如

```java
String s1 = new String("abc");
String s2 = new String("abc");
```

equlas()相等而hashCode()不相等。

当我们用这两个对象的hash值充当键值，放入hashMap或者HashSet去重时，发现两个对象的hashcode不一样，会存进去两个一样的对象。