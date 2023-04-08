---
title: "leecode-array"
subtitle: ""
date: 2023-04-08
draft: false
author: ""
authorLink: ""
description: "array刷题-continue"
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

1. 下标从 0 开始
2. 内存空间的地址连续 -> 会影响其他元素地址
3. 数组的元素无法删除，只能覆盖
4. 二维数组存内存的空间的地址是否连续？ -> 不同语言内存管理不一样 （C++连续 / java 不连续）

</br>

## 704. Binary Search

-> 给数组 nums + 升序 + 目标数 target
-> 找到数组中的目标数 target 返回其下标 index (无则-1)

```java
class Solution {
    public int search(int[] nums, int target) {

        if(nums == null || nums.length == 0) {
            return -1;
        }

        int l = 0;
        int r = nums.length - 1;


        while (l <= r) {
            int mid = l + (r-l) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] > target) {
                r = mid - 1;
            } else {
                l = mid + 1;
            }
        }

        return -1;

    }
}
```

1. nums == null 和 nums.length == 0 的区别

   - nums == null -> 数组为空此时 array 不指向任何对象 相当于 int[] array = null
   - nums.length == 0 -> 一个长度为 0 的数组 相当于 int[] array = new array[0]
   - 一般先判断 nums 是否为空，然后再判断长度是否为 0，因为可能报空指针异常

2. 二分法 -> 对撞双指针用法的规律
   - `nums[mid] == target` -> `return mid`
   - `nums[mid] > target` -> `r = mid - 1`
   - `nums[mid] < target` -> `l = mid + 1`

</br>

## 27. Removed Element

-> 给数组 nums + 目标数 val
-> 返回数组长度 length + 移除 val 之后的数组 nums (the order of elements may be changed)

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int l = 0;
        int r = nums.length - 1;

        while (l < r) {
            if (l < r && nums[l] != val ) {
                l++;
            }
            if (l < r && nums[r] == val) {
                r--;
            }
            int temp = nums[l];
            nums[l] = nums[r];
            nums[r] = temp;
        }
        return nums[l] == val? l : l+1;
    }
}
```

思路：

1. check 数组
2. 声明赋值 l / r -> 放置其在 nums 中的位置
3. 判断条件 l < r
   - 如果 l 遇到 var stop -> 也就是遇到其他值则 l++
   - 如果 r 遇到其他值 stop -> 也就是 r 遇到 var 则 r--
   - 置换 l 与 r 位置的值
4. 三元判断
   - 如果 = val 位置 则长度为 l + 1
   - 如果 >(!=) val 位置 则长度为 l

</br>

## 997. Square of a Sorted Array

=> 给数组 nums
=> 返回数组 + 每个数都平方

```java
class Solution {
    public int[] sortedSquares(int[] nums) {

        int l = 0;
        int r = nums.length - 1;
        int[] result = new int[nums.length];
        int k = result.length - 1;

        while (l <= r) {
            if (nums[l] * nums[l] < nums[r] * nums[r]) {
                result[k--] = nums[r] * nums[r];
                r--;
            } else {
                result[k--] = nums[l] * nums[l];
                l++;
            }
        }

        return result;

    }
}
```

思路：

1. 声明赋值 l / r -> 确定在 nums 的位置
2. 创建 result 新数组
3. 声明赋值 k -> 确定在 result 的位置
4. while 判断 left <= right 时候
   - 如果 `nums[l] * nums[l] < nums[r] * nums[r]` - > `result[k--] = nums[r] * nums[r]` 和 `r--`
   - 如果 `nums[l] * nums[l] > nums[r] * nums[r]` - > `result[k--] = nums[l] * nums[l]` 和 `r++`

</br>

## 209. Minimum Size Subarray Sum

=> nums(positive integers) + target(positive integers)
=> sum >= integer 的 minimal length of a subarray

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        if(nums == null || nums.length == 0) {
            return 0;
        }

        int res = nums.length + 1;
        int total = 0;
        int i = 0;
        int j = 0;

        while (j < nums.length) {
            total += nums[j];
            j++;

            while(total >= target) {
                res = Math.min(res, j - i);
                total -= nums[i];
                i++;
            }
        }

        return res == nums.length + 1 ? 0 : res;

    }
}
```

思路：

1. check array
2. 声明赋值 res / total / i / j
3. while 判断 j < nums.length 时候
   - 记录 total 滑动 j
   - 当 total >= target 时
     - 记录 res
     - 记录 total 滑动 i

注意：为什么 j-i 不用加 1，因为上一行 j++ 先移动了(细品)

</br>

## 59. Spiral Matrix II

=> positive integer n
=> generate an n \* n, filled with element from 1-n^2 in spiral order

```java
class Solution {
    public int[][] generateMatrix(int n) {
        //创建新二维矩阵
        int[][] res = new int[n][n];

        //边界
        int rowBegin = 0;
        int rowEnd = n-1;
        int columnBegin = 0;
        int columnEnd = n-1;

        int counter = 1;

        //四个
        while (rowBegin <= rowEnd && columnBegin <= columnEnd) {

            //从左到右 index 0 row不会 变动的是这一行的column
            for (int i = columnBegin; i <= columnEnd; i++) {
                res[rowBegin][i] = counter++;
            }
            rowBegin++;

            //从上到下 index n-1 column不变 变动的是这一列的row
            for (int i = rowBegin; i <=rowEnd; i++) {
                res[i][columnEnd] = counter++;
            }
            columnEnd--;

            if(rowBegin <= rowEnd) {
                //从右到左 index n-1 row不变 变动的是这一行的column
                for(int i = columnEnd; i >= columnBegin; i--) {
                    res[rowEnd][i] = counter++;
                }
            }
            rowEnd--;

            if(columnBegin <= columnEnd) {
                for(int i = rowEnd; i >= rowBegin; i--) {
                    res[i][columnBegin] = counter++;
                }
            }
            columnBegin++;

        }
        return res;
    }
}

```

</br>
