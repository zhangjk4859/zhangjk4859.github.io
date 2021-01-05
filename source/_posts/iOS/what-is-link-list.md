---
title: 链表是什么
date: 2021-01-06 00:23:22
categories: 
- iOS
tags:
---

**链表了解吗**

- Linked list is a sequence of links which contains items

- Link - Each link of a linked list can store a data called an element

- Next - Each link of a linked list contains a link to the next link called Next

- LinkedList - A Linked List contains the connection link to the first link called First

- Linked list can be visualized as a chain of nodes,where every node points to hte next node

  ![image](![Linked List](https://www.tutorialspoint.com/data_structures_algorithms/images/linked_list.jpg)

  - Simple linked list -item navigation is forward only
  - doubly linked list - items can be navigated forward and backward
  - circular linked list - last item contains link of the first element as next and the first element has a link to the last element as previous.

**双向链表是什么**

同上，节点有前后指针

**跟数组的区别**

- 数组在编译时已经分配好连续内存
- 链表在运行时添加数据时分配内存
- 数组在栈，链表在堆

**数组为什么快**

- 数组查找快，因为可以根据索引直接获得，复杂度O(1),链表复杂度O(N)
- 数组插入和删除慢，因为空间连续，插入删除后需要整理内存大小，链表插入删除快，只要改变指针指向即可

参考：1. https://www.tutorialspoint.com/data_structures_algorithms/linked_list_algorithms.htm

2.https://www.studytonight.com/data-structures/linked-list-vs-array