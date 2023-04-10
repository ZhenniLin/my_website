---
title: "leecode-linkedList"
subtitle: ""
date: 2023-04-10
draft: false
author: ""
authorLink: ""
description: "linkedList刷题-continue"
keywords: ""
license: ""
comment: false
weight: 0

tags:
  - leetcode
categories:
  - leetcode

hiddenFromHomePage: false
hiddenFromSearch: false

summary: ""
resources:
  - name: featured-image
    src: featured-image.jpg
  - name: featured-image-preview
    src: featured-image-preview.jpg

toc:
  enable: true
math:
  enable: false
lightgallery: false
seo:
  images: []
# See details front matter: /theme-documentation-content/#front-matter
---

<!--more-->

## Basic

1. 单链表

![Screenshot 2023-04-10 at 3.48.59 PM.png](https://s2.loli.net/2023/04/10/ConhMExby9waSQI.png)

- 通过指针串联在一起的线性结构
- 两个部分组成：数据域 + 指针域
- 最后一个指针节点指向 null (空指针)
- 入口节点为头节点 - head

2. 双链表

![Screenshot 2023-04-10 at 3.49.28 PM.png](https://s2.loli.net/2023/04/10/s5nrKVvZDk2be7B.png)

- 每个节点都有两个指针域分别指向上一个节点和下一个节点
- 既可以向前查询也可以向后查询

3. 链表的储存方式

- 链表在内存中不是连续分布的，而是散落在内存中的某地址上
- 链表通过指针域的指针链接在内存中各个节点

4. 链表的定义

```java
public class ListNode {
    // 结点的值
    int val;

    // 下一个结点
    ListNode next;

    // 节点的构造函数(无参)
    public ListNode() {
    }

    // 节点的构造函数(有一个参数)
    public ListNode(int val) {
        this.val = val;
    }

    // 节点的构造函数(有两个参数)
    public ListNode(int val, ListNode next) {
        this.val = val;
        this.next = next;
    }
}
```

5. 数组与链表

![Screenshot 2023-04-10 at 3.50.01 PM.png](https://s2.loli.net/2023/04/10/z82WFwTRBheHpmV.png)

- 数组：固定 / 查询
- 链表：不固定 / 增删

5. 疑惑点 (很重要的辨析！！！)

- 如果放在**等号左边**就表示是**自己的指向**
- 如果放在**等号右边**就表示是**它的下一个节点值**

</br>

## 203 Remove Linked List Elements

- the head of a linked list + integer val
- 移除 node.val == val + return the new head

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeElements(ListNode head, int val) {

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy;

        while (head != null) {
            if(head.val == val) {
                prev.next = head.next;
            } else {
                prev = head;
            }
            head = head.next;

        }
        return dummy.next;
    }
}
```

思路：

1. 创建一个新 listnode dummy 并赋值为 0
2. dummy.next 指向 head
   - 因为 head 相当于链表的第一个值
   - head 移动会丢失掉之前的值
   - 所以用 dummy 进行串联，head 就可以自由移动
3. 将 dummy 赋给 pre，因为初始状态下，dummy 是 head 的前一个 listnode
4. 如果 head.val == val -> 那么就将 head 前面一个 listnode 也就是 pre 的指针指向 head 后一个 listnode ；如果 head.val != val -> 那么就正常 prev 前进，将当前 head 赋给 prev
5. 然后 head 正常前进 head = head.next
6. return dummy.next

</br>

## 206 Removed Linked List Element

- the head of a linked list
- return the reversed list

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
// 双指针
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode cur = head;
        ListNode temp = null;
        while (cur != null) {
            temp = cur.next;// 保存下一个节点
            cur.next = prev;
            prev = cur;
            cur = temp;
        }
        return prev;
    }
}

```

思路：

1. 创建 listnode preve = null
2. 创建 listnode cur = head
3. 创建 listnode temp = null
4. 当 cur != null 时候
   - temp = cur.next 保存下一个节点值
   - cur.next = prev 指针翻转
   - prev = cur prev 移动
   - cur = temp cur 移动
5. renturn prev

</br>

## 02.07 Intersection of Two Linked Lists LCCI

- tow linked lists (if the two lists intersect)
- return the intersecting node

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode curA = headA;
        ListNode curB = headB;
        int lenA = 0, lenB = 0;

        while(curA != null) { //求链表A长度
            lenA++;
            curA = curA.next;
        }

        while(curB != null) { //求链表B长度
            lenB++;
            curB = curB.next;
        }

        //恢复重置
        curA = headA;
        curB = headB;

        //让curA为最长链表的头,lenA为其长度
        if(lenB > lenA) {
            //1. swap (lenA, lenB)
            int temLen = lenA;
            lenA = lenB;
            lenB = temLen;

            //2. swap (curA, curB)
            ListNode tmpNode = curA;
            curA = curB;
            curB = tmpNode;
        }

        //求长度差
        int gap = lenA - lenB;
        //同一起点 - 末尾位置对其
        while(gap-- > 0) {
            curA = curA.next;
        }
        //遍历两个linked list 如遇到相同则直接返回
        while(curA != null) {
            if (curA == curB) {
                return curA;
            }
            curA = curA.next;
            curB = curB.next;
        }
        return null;
    }
}
```

思路：

1. 求出两个链表的长度，让 curA 为长链表
2. 求两个链表之间的距离，设置两个链表为同一起点，让 curA 移动到和 curB 对其的位置
3. 比较 curA 和 curB 是否相同，不同则同时后移，如遇到 curA == curB, 则找到返回交点

</br>
