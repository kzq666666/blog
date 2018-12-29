---
title: "数据结构"
date: 2018-12-26T09:20:11+08:00
showDate: true
draft: false
tags: ["dataStructure", "structure"]
---

感谢邱老师这一个学期的数据结构课的教导，让我了解到什么是数据结构和其重要性，以及相关的算法和实现。
<br>这是一篇关于数据结构的复习。

## 基本概念

1.程序 = 算法 + 数据结构 &emsp; ------ Nicklaus Wirth
<br>一个程序就是通过具体的某种计算机语言将算法进行实现

2.数据结构：相互之间存在一种或多种特定关系的数据元素的集合
具体什么是数据结构，包含下面三个部分=>

- 逻辑关系：线性关系、非线性关系
- 存储方式：顺序存储、链接存储、散列存储
  <br>（存储存的除了要存数据，还要存它们之间的关系，这一点是邱老师在刚上数据结构讲这些基本概念的时候特别强调的，我印象挺深的）
- 运算集合：查找和排序（插入=>直接法，二分法、交换=>冒泡排序，快速排序、选择=>堆排序）

  3.算法：对特定问题求解步骤的一种描述。
  <br>一个算法还具有下列 5 个重要特性

- 有穷性&emsp;一个算法必须在执行有穷步之后结束，但一个程序则可以无穷，比如说无限死循环
- 确定性&emsp;算法的每一条指令必须有确切的含义
- 可行性&emsp;一个算法是能行的
- 输入&emsp;一个算法有零个或多个输入
- 输出&emsp;一个算法有一个或多个输出

<br>一个好的算法需要达到的目标

- 正确性
- 可读性
- 健壮性&emsp;当输入数据非法时，算法也能做出反应或进行处理，即要可以处理一些特殊和极端情况
- 效率和低存储量需求&emsp;时间复杂度低，算法执行时间短。满足需求的同时尽可能使用低的存储量消耗

  4.时间复杂度：&nbsp;算法中基本操作重复执行的次数是问题规模 n 的某个函数 f(n)，即
  T(n) = O(f(n))
  <br>5.空间复杂度：&nbsp;算法所需存储空间的量度，即 S(n)=O(f(n))

## 线性表

1.逻辑关系：线性关系/结构

- 存在唯一一个被称作"第一个"的数据元素
- 存在唯一一个被称作"最后一个"的数据元素
- 除第一个之外，集合中每个数据元素均只有一个前驱
- 除最后一个之外，集合中每个数据元素均只有一个后继

总的来说就是只有第一个元素有直接后继，没有前驱，只有最后一个元素有直接前驱，没有后继，在这两个元素之间的元素既有一个直接前驱也有一个直接后继

<br>2.存储方式和运算
<br>（1）顺序存储：用一组地址连续的存储单元依此存储线性表中的数据元素

```js
// 在JavaScript中，数组就是一种隐式的存储关系

// 初始化数组
function listInit() {
  return new Array();
}

// 插入=>第i-1个位置和第i个位置之间插入元素,i从1开始
function listInsert(list, i, data) {
  let len = list.length;
  if (i < 1 || i >= len + 1) {
    throw new Error("i的位置有误");
  }
  for (let j = len - 1; j >= i - 1; j--) {
    list[j + 1] = list[j];
  }
  list[i - 1] = data;
}

// 删除=>删除第i个位置的元素
function listDelete(list, i) {
  let len = list.length;
  if (i < 1 || i > len) {
    throw new Error("i的位置有误");
  }
  for (let j = i - 1; j <= len - 1; j++) {
    list[j] = list[j + 1];
  }
  // 切记不能用len--，因为是原始值，len改变并不会改变list.length
  list.length--;
}
```

（2）链式存储：用一组任意的存储单元存储线性表的数据元素（这组存储单元可以是连续的，也可以是不连续的）

- 一个结点包含两个域，一个是数据域，一个是指针域，此链表的每个结点中只包含一个指针域，故又称为线性链表或单链表

```js
// 单链表
var len = 0;
function linkListNode(data) {
  this.data = data;
  this.next = null;
}
headNode = new linkListNode(null);
// 获取第i个元素
function getElem(i) {
  var p = headNode.next;
  var j = 1;
  while (p && j < i) {
    p = p.next;
    j++;
  }
  return p ? p.data : null;
}
// 插入，在第i个位置之前插入元素e
function linkListInsert(linkListNode, i, e) {
  let newNode = new linkListNode(e);
  var j = 1;
  p = headNode;
  if (i < 1 || i > len + 1) {
    return new Error("i的范围有误");
  }
  while (j <= i - 1 && p.next) {
    p = p.next;
    j++;
  }
  newNode.next = p.next;
  p.next = newNode;
  len++;
}
// 删除，删除第i个位置的结点
function linkListDelete(i){
  var j = 1;
  pre = headNode;
  p = pre.next;
  while(j<i && p.next){
    pre = p;
    p = pre.next;
    j++;
  }
  if(j==i){
    return new Error('超出链表范围')
  }
  pre.next = p.next;
}
```
- 循环链表：表中最后一个结点的指针域指向头结点，整个链表形成一个环，从表中任一结点出发均可找到表中其他结点