---
title: "leecode-hashtable"
subtitle: ""
date: 2023-04-12
draft: false
author: ""
authorLink: ""
description: "linkedList 刷题-hashtable(array / hashmap / hashset)"
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

1. 根据关键码的值而进行访问的数据结构

- key: value -> 键值对

3. 一般解决问题：快速判断一个元素是否出现在合集里

4. 哈希函数

- key -> 哈希函数 -> 内存地址 -> key/value 对应的内存地址

5. 哈希碰撞

- 两个不同的 key 通过同一个哈希函数得到相同的内存地址
  - 方法 1: 拉链法 -> 发生冲突的元素都被存储在链表中
    - 拉链法就是要选择适当的哈希表的大小，这样既不会因为数组空值而浪费大量内存，也不会因为链表太长而在查找上浪费太多时间
  - 方法 2: 线性探测法 -> 要保证 tableSize 大于 dataSize，需要依靠哈希表中的空位来解决碰撞问题

6. 四个特性

访问 access：哈希表中没有

搜索 search：O(1)

- 通过 key 找 value
- 碰撞 O(k) -> k 就是碰撞元素的个数

插入 insert：O(1)

- key 直接通过哈希函数直接找到内存地址然后存入

删除 remove：O(1)

- key 直接通过哈希函数找到内存地址
- 删除值

7. 三种哈希结构

- **数组**
- **map 映射**
- **set 集合**

</br>

## 数组 Array

1. 数组 -> 就是一组哈希表

- 关键码 -> 数组索引下标
- 访问 -> 数组元素

2. hashtable 通过 数组 array 的常用操作

```java
//通过数组array - 创建哈希表
String[] hashTable = new String[4];

//添加元素
//time complexity: O(1)
hashTable[1] = "hanmeimei";
hashTable[2] = "lihua";
hashTable[3] = "siyangyuan";

//更新元素 update element
//time complexity: O(1)
hashTable[1] = "bishi";

//删除元素 remove element
//time complexity：O(1)
hashTable[1] = "";

//获取value get value
//time complexity:O(1)
String temp = hashTable[3];
```

</br>

## HashMap

1. 为什么有 hashmap ？

- HashMap 利用 hash 算法实现了快速存取的特性

2. hash table 和 HashMap 有什么关系？

- hash table 是一种逻辑数据结构，HashMap 是 Java 中的一种数据类型（结构类型），它通过代码实现了 Hash table 这种数据结构，并在此结构上定义了一系列操作

3. hashtable 通过 HashMap 的常用操作

```java
//创建哈希表
//通过编程语言自带的函数
HashMap<Integer, String> map = new HashMap<>();
//第一个是key的类型 第二个是value的类型

//添加元素 add elelments
//time complexity: O(1)
//map.put(key, value)
map.put(1, "hanmeimei");
map.put(2, "lihua");
map.put(3, "siyangyuan")

//更新元素 update element
//time complexity: O(1)
//map.put(key, value)
map.put(1,"bishi");

//删除元素 remove element
//time complexity：O(1)
//map.remove(key)
map.remove(1);

//获取value get value
//time complexity:O(1)
//返回与指定键关联的值
map.get(3);

//检查key是否存在 check key
//time complexity: O(1)
//hashTable check the length
//map.containsKey(key)
//返回值：如果Map集合中包含指定的键名，则返回true；否则返回false
map.containsKey(3);

//检查哈希表长度以及是否还有元素
//length
//time complexity: O(1)
//hashTable Size variables
map.size();

//Is Empty?
//time complexity:O(1);
//hashTable size variables
map.isEmpty();
```

</br>

## HashSet

1. set 集合的两个特点

- 无序
  - 里面的元素不是按照某个顺序而排序的
  - set 相当于 hash 表的 value，所以也算包含在 hash 表这个结构中
- 不重复
  - 里面的**所有元素都是独一无二的，不重复的**

2. set 的主要作用

- 检查某个元素是否存在
- 检查是否有重复元素
  - 对比 Num 原来数据集 ?= Num 插入集合
  - 如果 不等于 就说明存在重复元素

3. hashset 如何运作

![截屏2023-02-06 上午11.21.17.png](https://s2.loli.net/2023/02/06/Ew9uyRdJ4mYMfsv.png)
例如：现在要把一个元素加入一个 hashset 中

- 拿到元素
- 通过哈希函数得到这个元素的哈希值
- hashset 底部就是一个 hash 表，将哈希值放在哈希表上对应的位置
  - 如果对应位置没有元素 -> 存入对应位置
  - 如果应对位置有元素 -> 对比当前元素和哈希表上的元素是否相等
    - 如果是相等的 -> 重复，hashset 不允许重复，所以要么保留原来元素 or 进行更新
    - 如果是不相等的 -> 哈希冲突/碰撞，用之前提到的链表等方法

4. 四个特性

访问 access：在 set 里通过 index 进行访问是一个不太存在的方法 ❌

搜索 search： - 无 hash collision - O(1) ✅ - 有 hash collision - O(k) -> k 是冲突元素的个数

插入 insert： - 无 hash collision - O(1) ✅ - 有 hash collision - O(k)

删除 delete： - 无 hash collision - O(1) ✅ - 有 hash collision - O(k)

5. set 常用操作

```java
//create HashSet
HashSet<Integer> set = new HashSet<>();
//集合元素类型 变量名称 创建对象


//add element
//time complexity:O(1)
set.add(10);
set.add(3);
set.add(5);
set.add(2);
set.add(2);
//[10,3,5,2]
System.out.println(set.toString());


//search element
//O(1)
set.contains(2);


//delete element
//O(1)
set.remove(2);
//[10,3,5]
System.out.println(set.toString());


//size
//O(1)
set.size();
```

</br>

## HashMap 和 HashSet 的异同

![Screenshot 2023-04-12 at 6.28.59 PM.png](https://s2.loli.net/2023/04/12/xJ3isKbeg8Y2HZu.png)

</br>

## 242. Valid Anagram

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        int[] record = new int[26];

        for (int i = 0; i < s.length(); i++) {
            //charAt() 方法用于返回指定索引处的字符char值
            //索引范围为从 0 到 length() - 1
            //相互加减会得到ASCII码之间的运算
            record[s.charAt(i) - 'a']++; //不需要记住字符a的ASCII码，只需要一个相对字符即可
        }

        for (int i = 0; i < t.length(); i++) {
            record[t.charAt(i) - 'a']--;
        }

        for (int count: record) {
            if (count != 0) {
                return false;
            }
        }

        return true;

    }
}
```

</br>

## 349. Intersection of Two Arrays

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        if (nums1 == null || nums1.length == 0 || nums2 ==null || nums2.length == 0) {
            return new int[0];
        }

        Set<Integer> set1 = new HashSet<>();
        Set<Integer> resSet = new HashSet<>();

        //遍历数组nums1 将数传入set1
        for(int i : nums1) {
            set1.add(i);
        }
        //遍历数组nums2 如果发现nums2有与nums1重合的数 介入resSet
        for(int i : nums2) {
            if(set1.contains(i)) {
                resSet.add(i);
            }
        }

        //另外申请一个数组存放setRes中的元素，最后返回数组
        int[] arr = new int[resSet.size()];
        int j = 0;
        for (int i : resSet) {
            arr[j++] = i;
        }

        return arr;
    }
}
```

</br>

## 202. Happy Number

```
class Solution {
    public boolean isHappy(int n) {
        Set<Integer> record = new HashSet<>();
        //为了确保sum的重复出现，只要开始重复了就不进入循环
        while( n != 1 && !record.contains(n) ) {
            record.add(n);
            n = getNextNumber(n);
        }

        return n == 1;

    }

    private int getNextNumber(int n) {
        int res = 0;
        while(n > 0) {
            int temp = n % 10;
            res += temp * temp;
            n = n / 10;
        }
        return res;
    }
}
```

</br>

## 1. Two Sum

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] res = new int[2];
        if (nums == null || nums.length == 0) {
            return res;
        }

        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int temp = target - nums[i];
            if(map.containsKey(temp)) {
                res[1] = i;
                res[0] = map.get(temp);
                break;
            }

            map.put(nums[i], i);
        }
        return res;
    }
}
```

</br>

## 383. Ransom Note

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        //定义一个哈希映射数组
        int[] record = new int[26];

        //遍历
        for(char c : magazine.toCharArray()) {
            record[c - 'a'] += 1;
        }

        for(char c : ransomNote.toCharArray()) {
            record[c - 'a'] -= 1;
        }

        //如果数组中存在负数，说明ransomNote字符串中存在magazine中没有的字符
        for(int i : record) {
            if (i < 0) {
                return false;
            }
        }
        return true;
    }
}
```

</br>
