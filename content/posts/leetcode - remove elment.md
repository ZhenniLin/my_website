---
title: "leetcode｜array｜remove elements"
subtitle: ""
date: 2022-03-08T10:54:15+08:00
draft: false
author: ""
authorLink: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- array
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

<br>

## #27 remove element 

> 给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。
>
> 不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 原地 修改输入数组。
>
> 元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

[参考](https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html#_27-%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0)

注意事项：

- 数组的元素在内存地址中是连续的，不能单独删除数组中的某个元素，在删除或者增添元素的时候，就难免要移动其他元素的地址，所以只能覆盖

<br>

```java
class Solution {
    public int removeElement(int[] nums, int val) {

        // 快慢指针
        int fastIndex = 0;
        int slowIndex;
        for (slowIndex = 0; fastIndex < nums.length; fastIndex++) {
            if (nums[fastIndex] != val) {
                nums[slowIndex] = nums[fastIndex];
                slowIndex++;
            }
        }
        return slowIndex;

    }
}

```

<br>

### 疑问

1.`return slowIndex ` 到底return的是什么？即为什么最后输出的是修改后的数组？


<br>


## related questions 

<br>

### #26 Remove Duplicates from Sorted Array 

>给你一个 升序排列 的数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。元素的 相对顺序 应该保持 一致 。
>
>由于在某些语言中不能改变数组的长度，所以必须将结果放在数组nums的第一部分。更规范地说，如果在删除重复项之后有 k 个元素，那么 nums 的前 k 个元素应该保存最终结果。
>
>将最终结果插入 nums 的前 k 个位置后返回 k 。
>
>不要使用额外的空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。

参考：评论区修改

<br>

```java
class Solution {
    public int removeDuplicates(int[] nums) {

        int fastMove = 0;
        int slowMove;

        for (slowMove = 0; fastMove < nums.length; fastMove++) {
            if (nums[fastMove] != nums[slowMove] ) {
                nums[slowMove + 1] = nums[fastMove];
                slowMove++;
            }
        }
        return slowMove + 1;
    }
}

```

<br>

#### 疑问

1.为什么最后return的是 `return slowMove + 1;`

<br>

### #283 Move Zeroes

> 给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。
>
> **请注意** ，必须在不复制数组的情况下原地对数组进行操作。

参考：评论区修改Yanjun

思路：先移动 / 再给后边赋值0

<br>

```java
class Solution {
    public void moveZeroes(int[] nums) {

        int fastMove = 0;
        int slowMove;

        for (slowMove = 0; fastMove < nums.length; fastMove++) {
            if (nums[fastMove] != 0) {
                nums[slowMove] = nums[fastMove];
                slowMove++;
            }
        }

        for (int i = slowMove; i < nums.length; i++){
            nums[i] = 0;
        }
    }
}

```

