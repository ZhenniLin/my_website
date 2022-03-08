---
title: "leetcode｜array｜square of a sorted array"
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

## #977 Squares of a Sorted Array

>Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order 

[参考](https://programmercarl.com/0977.%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9.html#%E5%8F%8C%E6%8C%87%E9%92%88%E6%B3%95)

思路：双指针，在输入数组两头对比，然后对比结果依次输入结果数组，注意自增自减的含义

<br>

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        int[] result = new int[nums.length];
        int index = result.length -1;

        while (left <= right) {
            if (nums[right] * nums[right] > nums[left] * nums[left]) {
                result[index--] = nums[right] * nums[right];
                right--;
            } else { result[index--] = nums[left] * nums[left];
                left++;
            }
        }
        return result;
 }
}

```

