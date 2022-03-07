---
title: "leetcode|array|binary search"
subtitle: ""
date: 2022-03-07T10:54:15+08:00
draft: false
author: ""
authorLink: ""
description: "开始刷题"
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

## binary search

<br>

> 给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

 [参考](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.md) 

<br>

### 左闭右闭情况

```java

//使用二分查找的前提 - 无重复元素 + 有序数组 
//左闭右闭区间
class Solution {
    public int search(int[] nums, int target) {
        //避免target < num[0] or target > nums[nums.length-1]时多次运算
        if(target < nums[0] || target > nums[nums.length-1]) {
            return -1;
        }

        //确定初始左右下标值
        int left = 0, right = nums.length-1;
        //还是循环判断
        while(left <= right) {//总条件
        int mid = left + ((right - left) >> 1);
            if (nums[mid] == target) {//分条件1
                return mid;
            } else if (nums[mid] < target) {//分条件2
                left = mid + 1;
            } else if (nums[mid] > target) {//分条件3
                right = mid -1;
            }
        }
        return -1 

    }
}


```

<br>


### 左闭右开情况

```java

class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length;
        while (left < right) {
            int mid = left + ((right - left) >> 1);
            if (nums[mid] == target)
                return mid;
            else if (nums[mid] < target)
                left = mid + 1;
            else if (nums[mid] > target)
                right = mid;
        }
        return -1;
    }
}

```

<br>

### 疑问

1.((right - left) >> 1) / ((right - left) / 2)代表什么 

- 相当于重新中间的middle，用位移运算符，粗浅的理解为两端相减除以2
- right - left 是为了防止 integer overflow 现象 （如果你相加的话）

2.为什么第一种情况 right=left 是有意义的而第二种不是

- 第二种情况 - 因为left == right的时候，在[left, right)是无效的空间，所以只使用 < 
- 因为对于左闭右开的区间 `[2, 2)` 这种数值是无意义的， 所以当 `r = l` 的时候， 就该结束循环了， 所以只有在 `l < r` 才继续循环
- 因为对于左闭右闭的区间 [2, 2] 这种数值是有意义的（包含元素 2）， 所以当 r = l 的时候， 还有一个元素应该去查找， 所以 l <= r 继续循环

- 同样参考 [“循环不变量”](https://leetcode-cn.com/problems/binary-search/solution/er-fen-cha-zhao-de-xun-huan-bu-bian-liang-zhi-yao-/)

3.为什么第一种情况target right 的下标值是 nums.length-1 而第二种则是 nums.length

- 参考  [“循环不变量”](https://leetcode-cn.com/problems/binary-search/solution/er-fen-cha-zhao-de-xun-huan-bu-bian-liang-zhi-yao-/)
- 图解

<br>



## Related questions 

<br>

### Search-insert-position

> 给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。 - 三种写法

 [参考](https://programmercarl.com/0035.%E6%90%9C%E7%B4%A2%E6%8F%92%E5%85%A5%E4%BD%8D%E7%BD%AE.html)

<br>

```java

//暴力解法
class Solution {
    public int searchInsert(int[] nums, int target) {
            //目的
            //数组中找到目标值 并 返回索引
            //目标值不存在，插入数字最后并返回索引
        for(int i = 0; i < nums.length; i++) {
            if(nums[i] >= target) {
                return i;
            } 
        }
        
        return nums.length;
        
    }
}

```

```java


//左闭右闭解法
class Solution {
            //目的
            //数组中找到目标值 并 返回索引
            //目标值不存在，插入数字最后并返回索引
    public int searchInsert(int[] nums, int target) {
        //先判断初始左右
        int left = 0, right = nums.length - 1;

        while(left <= right) {
             int mid = left + ((right - left) >> 1);
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] > target) {
                right = mid - 1; 
            } else if (nums[mid] < target) {
                left = mid + 1;
            } 
        }
        return right + 1;
    }
}

```

```java


//左闭右开解法
class Solution {
            //目的
            //数组中找到目标值 并 返回索引
            //目标值不存在，插入数字最后并返回索引
    public int searchInsert(int[] nums, int target) {
        //先判断初始左右
        int left = 0, right = nums.length;

        while(left < right) {
             int mid = left + ((right - left) >> 1);
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] > target) {
                right = mid;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } 
        }
        return right ;
    }
}

```

<br>

### Search-for-range

> 给定一个包含 n 个整数的排序数组，找出给定目标值 target 的起始和结束位置。 如果目标值不在数组中，则返回`[-1, -1]`

 [参考](https://www.youtube.com/watch?v=R3HkgT2m_wg)

思路：分三块 - 主接收块 / 确定左边界块 / 确定右边界块 - 左边界块用 `num[mid] > target` 来促使往左边找，右边界块用 `num[mid] < target` 来促使从右边开始找

```java

class Solution {
    public int[] searchRange(int[] nums, int target) {
        int n = nums.length;
        int left = findFisrt(nums, target, n);
        int right = findLast(nums, target, n);
        return new int[]{left, right};
    }

    private int findFisrt(int[] nums, int target, int n) {
        int lo = 0, hi = n - 1;
        int index = -1;
        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] >= target) {
                hi = mid - 1;
            } else {
                lo = mid + 1;
            }
            if(nums[mid] == target) {
                index = mid; 
            }
        }
        return index;
    }

    private int findLast(int[] nums, int target, int n) {
        int lo = 0, hi = n - 1;
        int index = -1;
        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] <= target) {
                lo = mid + 1;
            } else {
                hi = mid - 1;
            }
            if(nums[mid] == target) {
                index = mid; 
            }
        }
        return index;
    } 

}

```
<br>




