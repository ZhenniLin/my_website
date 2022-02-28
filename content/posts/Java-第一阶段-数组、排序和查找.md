---
title: "Java-第一阶段-数组、排序和查找"
subtitle: ""
date: 2022-02-27T10:54:15+08:00
draft: false
author: ""
authorLink: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- Java
categories:
- 后端

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

## 数组

<br>

### 数组介绍

数组可以存放多个同一类型的数据。数组也是一种数据类型，是引用类型
即：数组就是一组数据

### 数组快速入门

```java

/**
 * 数组示例
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //定义一个数组
        //1 - double[] 表示 是double类型的数组 数组名 hens
        //2 - {3, 5, 1, 3.4, 2, 50}表示数组的值/元素，依次表示数组的第几个元素
        //
        double[] hens = {3, 5, 1, 3.4, 2, 50}; //也可以 double hens[]

        //遍历数组得到数组的所有元素的和 使用for
        //1 - 我们可以通过hens[下标]来访问数组的元素
        //    下标从0开始编号 比如第一个元素就是hens[0]
        //2 - 通过for就可以循环访问 数组的元素/值
        //3 - 使用变量totalWeight将各个元素累积
        System.out.println("===使用数组解决===");
        //提示：可以通过 数组名.length 得到数组的大小/长度
        //System.out.println("数组的长度=" + hens.length);
        double totalWeight = 0;
        for(int i = 0; i < hens.length; i++){
            System.out.println("第"+ (i+1) + "个元素的值=" + hens[i] );
            totalWeight += hens[i];
        }
        System.out.println("总体重=" + totalWeight + "平均体重="
                + (totalWeight / hens.length) );
    }
}

```

<br>

### 数组的使用

**1.使用方法1-动态初始化**

- 数组的定义

  - 数据类型 数组名[] = new 数据类型[大小]
  - int a[]=new int[5]; //创建了一个数组 名字a 存放5个int; 也可以int[] a =

- 数组的引用（使用/访问/获取数组元素）

  - 例如：你要是用a数组的第3个数 a[2]

```java

/**
* 数组示例
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //演示 数据类型 数组名[] = new 数据类型[大小]
        //循环输入5个成绩 保存在double数组 并输出

        //步骤
        //1 - 创建一个 double 数组，大小 5

        double[] score = new double[5];
        //2 - 循环输入
        //    score.length 表示数组的大小/长度
        //
        Scanner myScanner = new Scanner(System.in);
        for(int i = 0; i < score.length; i++){
            System.out.println("请输入第" + (i+1) + "个元素的值");
            score[i] = myScanner.nextDouble();
        }
        //输出，遍历数组
        System.out.println("===当前数组的元素/值情况如下：===");
        for( int i = 0; i < score.length; i++){
            System.out.println("请输入第" + (i+1) + "个元素的值=" + score[i]);
        }
    }
}

```

    <br>

**2.使用方法2-动态初始化**

- 先声明数组 

  - 语法：数据类型 数组名[]; 也可以 数据类型[] 数组名；
  - int a[]; 或者 int[] a;

- 创建数组

  - 语法： 数组名=new 数据类型[大小];
  - a=new int[10]

- 案例演示

```java

/**
* 数组示例
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //演示 数据类型 数组名[] = new 数据类型[大小]
        //循环输入5个成绩 保存在double数组 并输出

        //步骤
        //1 - 创建一个 double 数组，大小 5

        //(1)第一种动态分配方式
        //double scores[] = new doubles[5];
        //(2)第二种动态分配方式 先声明数组 再new，即分配空间

        double score[]; //声明一个数组 还没有分配空间 scores是nell
        score = new double[5];//分配内存空间，可以存放数据
        //2 - 循环输入
        //    score.length 表示数组的大小/长度
        //
        Scanner myScanner = new Scanner(System.in);
        for(int i = 0; i < score.length; i++){
            System.out.println("请输入第" + (i+1) + "个元素的值");
            score[i] = myScanner.nextDouble();
        }
        //输出，遍历数组
        System.out.println("===当前数组的元素/值情况如下：===");
        for( int i = 0; i < score.length; i++){
            System.out.println("请输入第" + (i+1) + "个元素的值=" + score[i]);
        }
    }
}

```

  <br>

**3.使用方式3-静态初始化**

- 初始化数组
  - 语法：数据类型 数组名[] = {元素值，元素值...}
  - int a[] = {2,5,6,7,8,89,90,34,56} 
- 快速入门案例
  - double hens[] = {3,5,1,3.4,2,50};
  - 等价
  - double hens[] = new double[6]；
  - hens[0] = 3; hens[1] = 5; hens[2] = 1; hens[3] = 3.4; hens[4] = 2; hens[5] = 50;
    <br>

### 数组使用注意事项和细节

1. 数组是多个相同类型的数据的组合，实现对这些数据的统一管理

2. 数组元素中可以是任何数据类型，包括基本类型和引用类型，但是不能混用

3. 数组创建后，如果没有赋值，有默认值
       int-0 short-0 byte-0 long-0 float-0.0 double-0.0
       char-\u0000 boolean-false String-null

4. 使用数组的步骤:
       声明数组并开辟空间
       给数组各个元素赋值
       使用数组

5. 数组的下标是从0开始的

6. 数组下标必须在指定范围内使用，否则报: 下标越界异常，比如int[ ] arr=new int[5];
       则有效下标为0-4

```java

int [] arr = new int[5];
System.out.println(arr[5]); //数组越界

```

7. 数组属引用类型，数组型数据是对象
   <br>

### 数组应用案例

1.创建一个char类型的26个元素的数组，分别放置‘A’-‘Z’，使用for循环访问所有元素并打印出来。提示：char类型数据运算‘A’+ 1 -> ‘B’

```java

/**
 * 数组示例
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        创建一个char类型的26个元素的数组，分别放置‘A’-‘Z’，
        使用for循环访问所有元素并打印出来 提示：char类型数据运算‘A’+ 1 -> ‘B’

        思路分析
        1 - 定义一个数组 char[] chars = new char[26]
        2 - 因为‘A’+ 1 -> ‘B’ 类推 使用for循环来赋值
        3 - 使用for循环访问所有元素

         */
        char[] chars = new char[26];
        for(int i = 0; i < chars.length; i++  ){ //循环26次
            // chars 是 char[]
            // chars[i] 是 char
            chars[i] = (char)('A'+ i);//'A'+ i 是int，需要强制转换
            //循环输出
            System.out.println(chars[i] + "");
        }
    }
}

```

2.求出一个数组int[ ]的最大值{4，-1，9，10，23}，并得到对应的下标

```java

/**
 * 数组示例
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        求出一个数组int[ ]的最大值{4，-1，9，10，23}，并得到对应的下标

        思路分析
        1 - 定义一个数组 int[] arr = {4，-1，9，10，23}
        2 - 假定 max = arr[0] 是最大值，maxIndex=0；
        3 - 从下标 1 开始遍历arr，如果max < 当前元素，说明max不是真正的最大值
            我们就 max = 当前元素；maxIndex = 当前元素下标
        4 - 当我们遍历整个数组arr后，max就是真正的最大值，maxIndex最大值对应的下标

         */

        int[] arr = {4,-1,9,10,23};
        int max = arr[0]; //假定第一个元素为最大值
        int maxIndex = 0;

        for(int i = 1; i < arr.length; i++){//从下标 1 开始遍历arr
            if(max < arr[i]){ // 如果max小于当前元素
                max = arr[i]; //把max设置成当前元素
                maxIndex = i;
            }
        }
        //当我们遍历这个数组arr后，max就是真正的最大值，maxIndex最大值下标
        System.out.println("max=" + max + " maxIndex=" + maxIndex);

    }
}

```

<br>

### 数组赋值机制

1. 基本数组类型赋值，这个值就是具体的数组，而且相互互不影响
   int n1 = 2; int n2 = 1; 

2. 数组在默认情况下是引用传递，赋的值是地址
   看一个案例，并分析数组赋值的内存图（重点）

```java

/**
* 数组示例
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //基本数据类型赋值 赋值方式为值拷贝
        //n2的变化 不会影响到n1的值
        int n1 = 10;
        int n2 = n1;

        n2 = 80;
        System.out.println("n1=" + n1); // 10
        System.out.println("n2=" + n2);

        //数组在默认情况下是引用传递 赋的值是地址，赋值方式为引用传递
        //是一个地址 arr2的变化是影响到arr1
        int[] arr1 = {1,2,3};
        int[] arr2 = arr1;//把arr1赋给arr2
        arr2[0] = 10;

        //看看arr1的值
        System.out.println("===arr1的元素===");
        for(int i = 0; i < arr1.length; i++){
            System.out.println(arr1[i]); // 10 2 3
        }
    }
}
//输出
/* n1=10
    n2=80
    ===arr1的元素===
    10
    2
    3
*/

```

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/17/fpXSWnH8zbwOaGU.jpg" alt="j101" >
</div>
{{</md>}}
<br>

### 数组拷贝

编写代码 实现数组拷贝（内容复制）
将 int[] arr1 = {10, 20, 30}; 拷贝到arr2数组，要求数据空间是独立的

```java

/**
* 数组示例
*/
public class Main {
//编写一个main方法
public static void main(String[] args) {
    // 将 int[] arr1 = {10, 20, 30}; 拷贝到arr2数组，要求数据空间是独立的

    int[] arr1 = {10,20,30};

    //创建一个新的数组arr2 开辟新的数据空间
    //大小 arr1.length;
    int[] arr2 = new int[arr1.length];
    
    //遍历arr1，把每个元素拷贝到arr对应的位置
    for(int i = 0; i < arr1.length; i++ ){
        arr2[i] = arr1[i];
        arr2[0] = 100;
        System.out.println(arr2[i]);
    }
}
}

```

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/17/ypWTOfAZzmvc9QR.jpg" alt="j102" >
</div>
{{</md>}}

<br>

### 数组反转

要求：把数组的元素内容反转
arr {11,22,33,44,55,66} -> {66,55,44,33,22,11}
// 思考
1）方式1 - 通过找规律反转 - 思路分析

```java

/**
 * 数组示例
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {

        //定义数组
        int[] arr = {11,22,33,44,55,66};
        //思路
        //1 - 把arr[0] 和 arr[5] 进行交换 {66,22,33,44,55,11}
        //2 - 把arr[1] 和 arr[4] 进行交换 {66,55,33,44,22,11}
        //3 - 把arr[2] 和 arr[3] 进行交换 {66,55,44,33,22,11}
        //4 - 一共交换3次 = arr.length / 2
        //5 - 每次交换时，对应下标 是 arr[i]和arr[arr.length - 1 -i]
        //代码
        //优化
        int temp = 0;
        int len = arr.length;//计算数组长度
        for(int i = 0; i < len / 2; i++){
            temp = arr[len - 1 -i];
            arr[len - 1 -i] = arr[i];
            arr[i] = temp;
        }
        System.out.println("====反转后的数组===");
        for(int i = 0; i < len; i++){
            System.out.print(arr[i] + "\t");//输出最新顺序
        }
        }
    }

```

2）方式2 - 使用逆序赋值方式 - 思路分析 学员自己完成

```java

/**
 * 数组示例
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {

        //定义数组
        int[] arr = {11,22,33,44,55,66};

        //逆序赋值方式
        //思路
        //1 - 创建一个新的数组 arr2 大小arr.length
        //2 - 逆序遍历arr，将每个元素拷贝进 arr2的元素中(顺序拷贝)
        //3 - 建议增加一个循环变量 j -> 0-5

        //代码
        int[] arr2 = new int[arr.length];
        for (int i = arr.length - 1, j = 0; i >= 0; i--, j++){
            //arr2[arr.length-1-i] = arr[i];
            arr2[j] = arr[i];
        }

        //4.当for循环结束，arr2就是一个逆序的数组 {66,55,44,33,22,11}
        //5.让arr 指向 arr2 数据空间,此时arr原来的数据空间就没有变量引用
        //  被当作垃圾销毁
        arr = arr2;

        System.out.println("===arr的元素情况===");
        //6.输出arr看看
        for(int i = 0; i < arr.length; i++){
            System.out.print(arr[i]+"\t");
        }

        }
    }

```

<br>

### 数组添加

要求：实现动态的给数组添加元素效果，实现对数组扩容
1）原始数组使用静态分配 int[] = {1,2,3}
2）增加的元素，直接放在数组的最后 arr={1,2,3,4} arrNew = {1,2,3,4}

```java

/**
 * 数组示例
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        要求：实现动态的给数组添加元素效果，实现对数组扩容
        1）原始数组使用静态分配 int[] = {1,2,3}
        2）增加的元素，直接放在数组的最后 arr={1,2,3,4} arrNew = {1,2,3,4}
        3）用户可以通过如下方法来决定是否继续添加，添加成功，是否继续 y/n

        思路分析
        1 - 定义初始数组 int[] arr = {1,2,3}
        2 - 定义一个新的数组 int[] arrNew = new int[arr.length+1];
        3 - 遍历arr数组，依次将arr的元素拷贝到arrNew数组
        4 - 将 4 赋值给 arrNew[arrNew.length - 1] = 4 //把4赋给arrNew最后一个元素
        5 - 让 arr 指向 arrNew -> arr = arrNew //那么原来的arr数组就被销毁
         */
        int[] arr = {1,2,3};
        int[] arrNew = new int[arr.length+1];
        for(int i = 0; i < arr.length; i++){
            arrNew[i] = arr[i];
        }
        //把4赋给arrNew最后一个元素
        arrNew[arrNew.length - 1] = 4;
        //让 arr 指向 arrNew
        arr = arrNew;
        //输出arr 看效果
        System.out.println("===arr扩容后元素情况===");
        for(int i = 0; i < arr.length; i++){
            System.out.print(arr[i]+"\t");
        }
        }
    }

```

3）用户可以通过如下方法来决定是否继续添加，添加成功，是否继续 y/n 

```java

import java.util.Scanner;
/**
 * 数组示例
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        要求：实现动态的给数组添加元素效果，实现对数组扩容
        1）原始数组使用静态分配 int[] = {1,2,3}
        2）增加的元素，直接放在数组的最后 arr={1,2,3,4} arrNew = {1,2,3,4}
        3）用户可以通过如下方法来决定是否继续添加，添加成功，是否继续 y/n

        思路分析
        1 - 定义初始数组 int[] arr = {1,2,3}
        2 - 定义一个新的数组 int[] arrNew = new int[arr.length+1];
        3 - 遍历arr数组，依次将arr的元素拷贝到arrNew数组
        4 - 将 4 赋值给 arrNew[arrNew.length - 1] = 4 //把4赋给arrNew最后一个元素
        5 - 让 arr 指向 arrNew -> arr = arrNew //那么原来的arr数组就被销毁
        6 - 创建一个Scanner可以接收用户输入
        7 - 因为用户什么时候退出，不确定，老师使用 do-while + break 来控制
         */

        Scanner myScanner = new Scanner(System.in);
        int[] arr = {1, 2, 3};

        do {
            int[] arrNew = new int[arr.length + 1];
            for (int i = 0; i < arr.length; i++) {
                arrNew[i] = arr[i];
            }
            System.out.println("请输入你要添加的元素");
            int addNum = myScanner.nextInt();
            //把addNum赋给arrNew最后一个元素
            arrNew[arrNew.length - 1] = addNum;
            //让 arr 指向 arrNew
            arr = arrNew;
            //输出arr 看效果
            System.out.println("===arr扩容后元素情况===");
            for (int i = 0; i < arr.length; i++) {
                System.out.print(arr[i] + "\t");
            }
            //问用户是否继续
            System.out.println("是否继续添加 y/n");
            char key = myScanner.next().charAt(0);
            if(key != 'y'){ //如果输入n 就结束
                break;
            }
        } while (true);
        System.out.println("你退出了添加");
    }
}
//数组扩容较慢 - 每次都要开辟新的一个数组 - 后边数据结构 链表 会较为方便

```

<br>

### 数组缩减

课后练习题
有一个数组{1,2,3,4,5}, 可以将该数组进行缩减，提示用户是否继续缩减，每个缩减最后哪个元素。当只剩下最后一个元素，提示，不能再缩减

```java

import java.util.Scanner;
/**
 * 数组示例
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        要求：
           有一个数组{1,2,3,4,5}, 可以将该数组进行缩减，
           提示用户是否继续缩减，每个缩减最后哪个元素。
           当只剩下最后一个元素，提示，不能再缩减

        思路分析
        1 - 定义初始数组 int[] arr = {1,2,3,4,5} //下标0-4
        2 - 定义一个新的数组 int[] arrNew = new int[arr.length-1];
        3 - 遍历arr数组，依次将arr的元素拷贝到arrNew数组
        4 - 让 arr 指向 arrNew -> arr = arrNew //那么原来的arr数组就被销毁
        5 - 创建一个Scanner可以接收用户输入 - 缩减
        6 - 因为用户什么时候退出，不确定，老师使用 do-while + break 来控制
         */
        Scanner myScanner = new Scanner(System.in);
        //数组初始化
        int [] arr = {1,2,3,4,5};

         do{
            int[] arrNew = new int[arr.length-1];
            //遍历arr数组，依次将arr的元素拷贝到arrNew数组
            for(int i = 0; i < arrNew.length; i++){
                arrNew[i] = arr[i];
            }
            arr = arrNew;
            // 输出arr 看效果
            System.out.println("===arr缩减后元素情况===");
            for(int i = 0; i < arrNew.length; i++){
                System.out.print(arr[i] + "\t");
            }
            //问用户是否继续
            System.out.println("是否继续缩减 y/n");
            char key = myScanner.next().charAt(0);
            if (key != 'y' && arr.length != 1){
                System.out.println("你退出了添加...");
                break;
            } else if (arr.length == 1){
                System.out.println("只有一个元素，不能再缩减");
                break;
            }
        } while (true);
         
    }
}

```

<br>

<hr>


## 排序

<br>

### 排序介绍

排序是将多个数据，依指定的顺序进行排列的过程
排序的分类：

1. 内部排序：
   指将需要处理的所有数据都加载到内部存储器中进行排序。包括（交换式排序法、选择式排序法和插入式排序法）
2. 外部排序法：
   数据量过大，无法全部加载到内存中，需要借助外部存储进行排序。包括（合并排序法和直接合并排序法）
   <br>

### 冒泡排序法

冒泡排序（bubble sorting）的基本思想：通过对待排序序列从后向前（从下标较大的元素开始），依次比较相邻元素的值，若发现逆序则交换，使值较大的元素逐渐从前向后部，就像水底下的气泡一样逐渐向上冒 

1. 冒泡排序法案例
   我们将五个无序：24，69，80，57，13 使用冒泡排序法排成一个从小到大的有序数列

{{<md>}}
  <div align="center">
  <img src="https://s2.loli.net/2022/02/17/BEA5GWZsKL2e9On.jpg" alt="j103" >
  </div>
{{</md>}}

```java

/**
 * 数组示例
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        要求：我们将五个无序：24，69，80，57，13 使用冒泡排序法排成一个从小到大的有序数列

        化繁为简 先死后活

        将多轮排序使用外层循环包括即可

         */
        int[] arr = {24,69,80,57,13,-1,30,200,-110};
        int temp = 0; //用于辅助交换的变量
        //将多轮排序使用外层循环包括起来即可
        //先死后活 -> 4 = arr.length - 1
        for(int i = 0; i < arr.length - 1; i++){ // 外层循环是4次
            for(int j = 0; j < arr.length - 1 - i; j++){//4次比较 -3次-2次-1次
                //如果前面的数>后面的数, 就交换
                if(arr[j] > arr[j + 1]){
                    temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
            }
            System.out.println("\n==第"+(i+1)+"轮==");
            for(int j = 0; j < arr.length; j++){
                System.out.print(arr[j]+"\t");
            }
        }
	}
}

```

<br>

<hr>


## 查找

<br>

介绍：

在java中，我们常用的查找有两种：

1.顺序查找

2.二分查找 - 二分法，我们放在算法讲解



案例演示

1.有个数列：白眉魔王、金毛狮王、紫衫龙王，轻翼蝠王猜数游戏：从键盘中任意输入一个名称，判断数列中是否包含此名称【顺序查找】要求：如果找到了，就提示找到，并给出下标值

```java

/**
 * 数组示例
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        要求：有个数列：白眉魔王、金毛狮王、紫衫龙王，轻翼蝠王猜数游戏：从键盘中任意输入一个名称，
        判断数列中是否包含此名称【顺序查找】要求：如果找到了，就提示找到，并给出下标值

        思路分析：
        1 - 定义一个字符串数组
        2 - 接收用户输入，遍历数组，逐一比较
            如果有，则提出信息并退出
         */

        String[] names = {"白眉魔王","金毛狮王","紫衫龙王","轻翼蝠王"};
        Scanner myScanner = new Scanner(System.in);

        System.out.println("请输入名字");
        String findName = myScanner.next();

        int index = -1;
        for(int i = 0; i < names.length; i++){
            //比较字符串
            //编程思想/技巧 - 经典方法
            if(findName.equals(names[i])){
                System.out.println("恭喜你找到"+findName);
                System.out.println("下标为="+ i);
                index = i;
                //把 i 保存到 index
                break;
            }
        }
            if(index == -1){//没有找到
                System.out.println("抱歉，未找到"+findName);
            }

        }

    }

```

2.请对一个有序数列进行二分查找{1,8,10,89,1000,1234}，输入一个数看看该数组是否存在此数，并且求出下标，如果没有就提示“没有这个数”

<br>

<hr>


## 多维数组 - 二维数组

<br>

多维数组只介绍二维数组

二维数组的应用场景 - 开发一个五子棋游戏，棋盘就是需要二维数组来表示

<br>



### 二维数组的使用

<br>

案例

```java

/**
 * 二维数组示例
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        请用二维数组输出如下图形
        0 0 0 0 0 0
        0 0 1 0 0 0
        0 2 0 3 0 0
        0 0 0 0 0 0
         */
        //什么是二维数组：
        //1.从定义形式上来看 int[][]
        //2.可以这样理解，原来的一维数组的每个元素是一维数组，就构成二维数组
        int[][] arr = {{0,0,0,0,0,0 },{0,0,1,0,0,0}, //二维数组的每个元素都是一维数组
                {0,2,0,3,0,0},{0,0,0,0,0,0}};
      	//第一个[]表示二维数组里有几个一维数组，第二个[]表示每个一维数组的下标
      	//外边大的是二维数组，里边小的是一维数组
        
      //关于二维数组的关键概念
      	//1.
      	System.out.println("二维数组的元素个数"+ arr.length);//四个
      	//2.二维数组的每个元素是一维数组，如果需要得到每个一维数组的值，还需再次遍历
      	//3.如果我们要访问第(i+1)个一维数组的第(j+1)个值 arr[i][j]
      	//  举例 访问3 -> 是第3个一维数组的第4个值 arr[2][3]
      	System.out.println(“第三个一维数组的第四个值”+ arr[2][]3);
      	
      
        //输出二维图形
      	//先输出二维数组中的元素(一维数组)，一维数组再相应输出自己数组内的元素，循环往复
        for(int i = 0; i < arr.length; i++){//遍历二维数组的每个元素
            //遍历二维数组的每个元素(数组)
            //解读
            //1 - arr[i]表示 二维数组的第(i+1)个元素，比如arr[0]：二维数组的第一个
            //1 - arr[i].length得到 对应的 每个一维数组的长度
            for(int j = 0; j < arr[i].length; j++){
                System.out.print(arr[i][j]+"\t");
            }
            System.out.println();//换行
        }
        }
    }

```

<br>

1.使用方式1: 动态初始化

- 语法：类型[] [] 数组名=new 类型[大小] [大小]

- 比如 `int a[][]=new int[2][3]`  - 两个一维数组，每个一维数组有3个元素

```java

/**
* 二维数组示例
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        int arr [][]=new int[2][3];
        arr[1][1] = 8;
        //遍历arr数组
        for(int i = 0; i < arr.length; i++){
            for(int j = 0; j < arr[i].length; j++){
                System.out.print(arr[i][j] + " " );
            }
            System.out.println();//换行
        }
        
    }

    }
// 0 0 0 
// 0 8 0 

```

<br>

2.使用方式2: 动态初始化

- 先声明：类型 数组名[] [] 

- 再定义 (开辟空间) 数组名 = new 类型[大小] [大小]

- 赋值(有默认值，比如int，类型的就是0)

- 使用演示

  `int arr[][]`

  `arr = new int[2][3]`

  <br>

3.使用方式3：动态初始化-列数不确定

- 看一个需求：动态创建下面二维数组，并输出

- 完成该案例

```java

/**
* 二维数组示例
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        看一个需求：动态创建下面二维数组，并输出
        i = 0：1
        i = 1：2 2
        i = 2：3 3 3

        一共有三个一维数组，每个一维数组的元素以及个数是不一样的
        */
        int[][] arr = new int[3][]; //创建二维数组，只是确定一维数组的个数，但是一维数组本身是null没有开数据空间
        for(int i = 0; i < arr.length; i++){ //遍历arr每个一维数组
            //给每个一维数组开空间 new
            //如果没有给一维数组new，那么arr[i]就是null
            arr[i] = new int[i+1];

            //遍历一维数组，并给一维数组的每个元素赋值
            for(int j = 0; j < arr[i].length; j++){
                arr[i][j] = i + 1; //赋值
            }
        }
        System.out.println("===arr元素===");
        //遍历arr输出
        for(int i = 0; i < arr.length; i++){
            //输出arr的每个一维数组
            for(int j = 0; j < arr[i].length; j++){
                System.out.print(arr[i][j] + " ");
            }
            System.out.println();
        }


    }

    }

```

<br>

4.使用方式4: 静态初始化

- 定义 - 类型 数组名[] [] = {{},{},..}

- 使用即可 

  `int[][] arr = {{1,1,1},{8,8,9},{100}};`

  定义了一个二维数组 arr

  arr有三个元素 - 每个元素都是一堆数组

  第一个一维数组有3个元素，第二个一维数组有3个元素，第三个一维数组有1个元素

<br>



### 二维数组的遍历

```java

/**
 * 二维数组练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        int arr[][] = {{4.6},{1,4,5,7},{-2}} 遍历二维数组，并得到和

        思路
        1 - 遍历二维数组，并将各个值累积到 int sum
         */
        int arr[][] = {{4,6},{1,4,5,7},{-2}};
        int sum = 0;
        for(int i = 0; i < arr.length; i++){
            for(int j = 0; j < arr[i].length; j++){
                System.out.print(arr[i][j] + " ");
                sum += arr[i][j];
            }
            System.out.println();
            System.out.println("sum=" + sum);
        }
    }
    }

```

<br>



### 二维数组的应用案例

```java

/**
 * 二维数组 - 杨辉三角 练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        1
        1 1
        1 2 1
        1 3 3 1
        1 4 6 4 1
        1 5 10 10 5 1

        规律
        1 - 第一行有1个元素，第n行有n个元素
        2 - 每一行的第一个元素和最后一个元素都是1
        3 - 从第三行开始，对于一个非第一个元素和最后一个元素的值 arr[i] [j]
            arr[i][j] = arr[i-1][j] + arr[i-1][j+1]; //必须找到这个规律
        */

        int[][] yangHui = new int[10][];
        for(int i = 0; i < yangHui.length; i++){//遍历yangHui的每个元素
            //给每个一维数组开空间
            yangHui[i] = new int[i+1];
            //给每个一维数组(行)赋值
            for(int j = 0; j < yangHui[i].length; j++){
                //每一行的第一个元素和最后一个元素都是1
                if(j == 0 || j == yangHui[i].length - 1){
                    yangHui[i][j] = 1;
                } else {//中间的元素
                    yangHui[i][j] = yangHui[i-1][j] + yangHui[i-1][j-1];
                }
            }

        }
        //输出杨辉三角
        for(int i = 0; i < yangHui.length; i++){
            for(int j = 0; j < yangHui[i].length; j++){//遍历输出该行
                System.out.print(yangHui[i][j] + " ");
            }
            System.out.println();//换行
        }

    }

    }

```

<br>



### 二维数组使用细节和注意事项

<br>

1.一维数组的声明方式

- int [] 或者 int x[]

2.二维数组的声明方式有

- int[] [] y 或者 int[] y[] 或者int y[] []

3.二维数组实际上是由多个一维数组组成的，它的各个一维数组的长度可以相同，也可以不相同。比如：map[] [] 是一个二维数组 

- int map[] [] = {{1,2},{3,4,5}}

- 由map[0] 是一个含有两个元素的一维数组，map[1]是一个含有三个元素的一维数组构成，我们也称为列数不等的二维数组

<br>

<hr>


### 二维数组课堂练习

{{<md>}}
  <div align="center">
  <img src="https://s2.loli.net/2022/02/17/gf74sOax8HjL6CI.jpg" alt="j104" >
  </div>
{{</md>}}

<br>

<hr>


### 本章作业

<br>

{{<md>}}
  <div align="center">
  <img src="https://s2.loli.net/2022/02/17/4Ls8tloH3TSGZxc.jpg" alt="j105" >
  </div>
{{</md>}}



```java

/**
 * 数组章节练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        已知有个升序的数组，要求插入一个元素，该数组顺序依然是升序，比如：
        [10,12,45,90], 添加23后，数组为[10,12,23,45,90]

        思路 数组扩容+定位
        1 - 先确定添加的数应该插入到哪个索引
        2 - 然后扩容
        */

        //先定义原数组
        int[] arr = {10,12,45,90};
        int insert = 23;
        int index = -1;//index就是要插入的位置

        //遍历 arr数组，如果发现 insertNum <= arr[i], 说明i就是要插入的位置
        //使用index 保留 index = i;
        //如果遍历完后，没有发现 insertNum <= arr[i]，说明index = arr.length
        //即: 添加到arr的最后

        for(int i = 0; i < arr.length; i++){
            if (insert <= arr[i]){
                index = i;
                break;//找到位置后就退出
            }
        }
        //判断index的值
        if(index == -1){ //说明还没有找到位置
            index = arr.length;
        }

        System.out.println("index=" + index);

        //扩容
        //先创建一个新的数组 大小arr.length+1
        int[] arrNew = new int[arr.length + 1];
        //准备将arr的元素拷贝到arrNew, 并且要跳过index位置
        /*
        分析：
        int[] arr = {10, 12, 45, 90};
        arrNew = {             }
         */
        //i是指向
        for(int i = 0, j = 0; i < arrNew.length; i++){
            if( i != index){
                arrNew[i] = arr[j];
                j++;
            } else { //这个位置就是要插入的数
                arrNew[i] = insert;
            }
        }
        //让arr指向arrNew 原来的数组无用销毁
        arr = arrNew;
        System.out.println("===插入后，arr数组的元素情况======");
        for(int i = 0; i < arr.length; i++){
            System.out.print(arr[i] + "\t");
        }

    }

    }

```



```java

/**
 * 数组章节练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        随机生成10个整数(1-100的范围)保存到数组，
        并倒序打印以及求平均值、求最大值和最大值的下标、
        并查找里面是否有8
        */

        //先定义原数组

        int[] arr = new int[10];
        //(int)(Math.random() * 100) + 1 生成 1 - 100
        for(int i = 0; i < arr.length; i++ ){
            arr[i] = (int)(Math.random() * 100) + 1;
        }

        System.out.println("===arr的元素情况===");
        for(int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + "\t" );
        }

        System.out.println();
        System.out.println("===arr的元素情况(倒序)===");
        for(int i = arr.length - 1; i >= 0; i--){
            System.out.print(arr[i] + "\t");
        }

        //平均值、求最大值和最大值的下标
        //我们这里需要一起完成
        //
        double sum = arr[0];
        int max = arr[0];
        int maxIndex = 0;

        for(int i = 1; i < arr.length; i++){

            sum += arr[i];

            if( max < arr[i]) { //说明max不是最大值 变化
                max = arr[i];
                maxIndex = i;
        }

        }
        System.out.println("\nmax=" + max + "\t" + "maxIndex=" + maxIndex);
        System.out.println("平均值=" + sum / arr.length);

        //查找数组中是否有8 -> 使用顺序查找
        int findNum = 8;
        int index = -1; //如果找到，就把下标记录到index
        for(int i = 0; i < arr.length; i++){
            if(findNum == arr[i]){
                System.out.println("找到数" + findNum + "下标=" + i);
                index = 1;
                break;
            }
        }
        if(index == -1){
            System.out.println("没有找到数" + findNum);
        }


    }

    }
```

```java
/**
 * 数组章节练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        冒泡排序
        要求从小到大
        要求从大到小
        */

        int[] arr = {20, -1, 89, 2, 890, 7};
        int temp = 0;
        for(int i = 0; i < arr.length -1; i++){
            for(int j = 0; j < arr.length -1 - i; j++){
                //如果是从小到大 条件是 arr[j] > arr[j+1]
                //如果是从大到小(arr[j] < arr[j+1]
                if(arr[j] > arr[j+1]){
                    temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
            }
        }
        System.out.println("\n===排序后===");
        for(int i = 0; i < arr.length; i++){
            System.out.print(arr[i] + "\t");
        }

    }

    }

```

<br>

<hr>


