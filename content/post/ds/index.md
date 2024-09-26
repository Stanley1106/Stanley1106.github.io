---
title: "Data Structure Note"
description: 
date: 2024-09-26T11:43:26+08:00
image: 
categories:
    - School
tags:
    - DS
    - Note
math: 
slug: ds-note
license: 
hidden: false
comments: false
draft: false
---
# DS 筆記
## 演算法
[Breadth-First Search(BFS)](https://www.cs.usfca.edu/~galles/visualization/BFS.html)
廣度優先，用queue依序找每個階層，如果此點紀錄為已走過，並回到上一個基準節點去尋找其他與基準節點相鄰的點

[Depth-First Search(DFS)](https://www.cs.usfca.edu/~galles/visualization/DFS.html)
深度優先，線性往下找，注意的是走訪過的節點不能再度走訪，所以使用堆疊stack後進先出的特性來記錄還沒有走過的節點

## Heap
1. [Min Heap/Max Heap](https://www.cs.usfca.edu/~galles/visualization/Heap.html)
    放入時都是放在最後，將小(大)的往上排，大(小)的往下放
2. [Heap sort](https://www.cs.usfca.edu/~galles/visualization/HeapSort.html)
    從下面開始比較，下面若比上還大，做交換，最後把最上方提出

## Tree 特性
* full tree
一個高度為3的完滿二元樹，會有7個節點
* complete tree
一個高度為3的完滿二元樹，會小於7個節點
由上到下，由左至右，沒有空格
* balance tree
平衡二元樹指的是，任意一個節點底下的兩顆子樹，子樹深度差不超過 1(最多能差 1 層的意思)。
    
## Graph 圖形
(島與島)
spanning tree
![image](https://hackmd.io/_uploads/HJPrgG4va.png)
## Hash 雜湊
在用雜湊函數運算出來的雜湊值，根據鍵 (key)來儲存在數據結構中。而存放這些記錄的數組就稱為雜湊表。

## Binary Tree Traversal
![image](https://hackmd.io/_uploads/r1nIefEPa.png)
* 前序 (preorder): 中 -> 左 -> 右，4213657
* 中序 (inorder): 左 -> 中 -> 右，1234567。注意：對二元搜尋樹 (binary search tree, BST) 做 inorder traversal 就是由小到大依序遍歷。
* 後序 (postorder): 左 -> 右 -> 中，1325764

## 2-3 Tree
https://z1nhouse.github.io/post/5lQAWUQWk/

## AVL Tree
平衡樹