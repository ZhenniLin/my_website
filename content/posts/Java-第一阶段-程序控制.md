---
title: "Java-第一阶段-程序控制"
subtitle: ""
date: 2022-02-27T10:54:15+08:00
draft: false
author: ""
authorLink: ""
description: "各类语句关键字要掌握"
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

<!--more-->

在程序中，程序运行的流程控制决定程序是如何执行的，是我们必须掌握的，主要有三大流程控制语句

- 顺序控制
- 分支控制
- 循环控制

---

## 顺序控制

<br>

### 顺序控制介绍

程序从上到下逐行执行，中间没有任何判断和跳转

### 顺序控制距离和注意事项

Java中定义变量时采用合法的向前饮用 如：

```java

public class Test{
    int num1 = 12;
    int num2 = num1+2;
}
错误形式：
public class Test{
    int num2 = num1 + 2; //错误
    int num1 = 12； 
}

```

<br>

<hr>


## 分支控制 (if else switch)

<br>

### 分支控制if-else介绍

让程序有选择的执行，分支控制有三种

- 单分支
- 双分支
- 多分枝

**1.单分支**

- 基本语法

```java

if (条件表达氏){
    执行代码块；(可以有多条语句)
}

```

- 说明：当条件表达式为true时，就会执行{}的代码。如果为false，就不执行。特别说明，如果{}中只有一条语句，则可以不用{}，建议写上{}

- 案例说明：编写一个程序，可以输入人的年龄，如果该同志的年龄大于18岁，则输出“你年龄大于18，要对自己的行为负责”

``` java

import java.util.Scanner;
/**
* 演示if语句
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
    //编写一个程序，可以输入人的年龄，如果该同志的年龄大于18岁
    //则输出“你年龄大于18，要对自己的行为负责”
    //思路分析
    //1.接收输入的年龄，应该定义一个Scanner 对象
    //2.把年龄保存到一个变量 int age
    //3.使用if判断，输出对应信息
        Scanner myScanner = new Scanner(System.in);
        System.out.println("请输入年龄");
        int age = myScanner.nextInt();
        if(age > 18){
            System.out.println("你的年龄大于18岁，要对自己的行为负责");
        }
        System.out.println("程序继续执行....");
    }
}

```

- 单分支对应的流程图
{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/12/6fiJza4DUVpsmyR.jpg" alt="j201" >
</div>
{{</md>}}

**2.双分支**

- 基本语法

```java

if (条件表达式){
    执行代码块1；
}
else{
    执行代码块2
}

```

- 说明：当条件表达式成立，即执行代码块1，否则执行代码块2

- 案例演示：编写一个程序，可以输入人的年龄，如果该同志的年龄大于18岁，则输出“你年龄大于18，要对自己的行为负责”。否则，输出“您还未到达法定年龄18岁”

```java

import java.util.Scanner;
/**
* 演示if语句
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
    //编写一个程序，可以输入人的年龄，如果该同志的年龄大于18岁
    //则输出“你年龄大于18，要对自己的行为负责”
    //思路分析
    //1.接收输入的年龄，应该定义一个Scanner 对象
    //2.把年龄保存到一个变量 int age
    //3.使用if-else判断，输出对应信息
        Scanner myScanner = new Scanner(System.in);
        System.out.println("请输入年龄");
        int age = myScanner.nextInt();
        if(age > 18){
            System.out.println("你的年龄大于18岁，要对自己的行为负责");
        } else{
            System.out.println("你的年龄还未到达法定年龄18岁");
        }
        System.out.println("程序继续执行....");
    }
}

```

- 双分支对应流程图
{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/12/Q6EbjkFWCnYyItU.jpg" alt="j202" >
</div>
{{</md>}}

**3.单分支和双分支练习题**

- 第一题
{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/12/JOGEFjnmrA9K2z6.jpg" alt="j203" >
</div>
{{</md>}}

- 第二题：编写程序，声明2个double型变量并赋值。判断第一个数大于10.0，且第二个数小于20.0，打印两数之和

```java

/**
* 演示单分支和双分支的练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
    double a = 3.3;
    double b = 5.2;
    if(a > 10.0 && b < 20){
        System.out.println("两数目之和=" + ( a + b ));;
        }else {
        System.out.println("无法执行噢～");
    }
    }
}

```

- 第三题：定义两个变量int 判断二者的和 是否能被3又能被5整除 打印提示信息    

```java

/**
* 演示单分支和双分支的练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
    int a = 8;
    int b = 12;
    int c = a + b;
    if(c % 5 == 0 && c % 3 == 0){
        System.out.println("很成功噢");
    } else {
            System.out.println("不太成功噢");
        }
    }
}

```

- 第四题：判断一个年份是否是闰年，闰年的条件是复合下面二者之一：年份能被4整除，但不能被100整除 / 能被400整除 

```java

import java.util.Scanner; //自己用了Scanner～
/**
* 演示单分支和双分支的练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
    Scanner myScanner = new Scanner(System.in);
    System.out.println("输入年份啦～");
    int year = myScanner.nextInt();
    if((year % 4 == 0 && year % 100 != 0) || year % 400 == 0){
        System.out.println("是闰年噢");
    } else {
            System.out.println("不是闰年噢");
        }
    }
}

```

**4.多分支**

- 基本语法 

```java

if (条件表达式1){
    执行代码块1；
}
else if (条件表达式2){
    执行代码块2；
}
....
else{
    执行代码块n；
}
// 多分支可以没有else，如果所有的条件表达式都不成立，则一个执行入口都没有
// 如果有else，如果所有的条件表达式都不成立，则默认执行else代码块

```

- 多分支流程图

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/12/gkINmSiZcPb5XVl.jpg" alt="j204" >
</div>
{{</md>}}

  - 当条件表达式1成立时，即执行代码块1
  - 如果表达式1不成立，才去判断表达式2是否成立
  - 如果表达式2成立，就执行代码块2
  - 以此类推，如果所有的表达式都不成立
  - 则执行else的代码块，注意，只能有一个执行入口    

**5.多分支练习**

- 第一题：输入Kara的信用分：如果：信用为100分 输出 信用极好；信用为(80.90]时，输出信用优秀；信用分为[60 ,80]时，输出 信用一般；其他情况，输出 信用不及格；请从键盘输入Kara的信用分，并加以判断

```java

import java.util.Scanner;
/**
* 演示多分支练习(双分支里嵌入里一个多分支)
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
    Scanner myScanner = new Scanner(System.in);
    System.out.println("请输入你的名字啦");
    String name = myScanner.next();
    System.out.println(name+"，您好呀，接下来请输入您的信用分～");
    //思考：如果使用者输入的不是整数，而是hello..
    //==>这里我们后面可以使用异常处理机制搞定
    int point = myScanner.nextInt();
    // 先对输入的信用分，进行一个范围的有效判断 1-100 否则提示输入错误
    if(point >= 1 && point <= 100) {
        if (point == 100) {
            System.out.println("你的信用超好的er！");
        } else if (point > 80 && point <= 90) {
            System.out.println("你的信用优秀棒棒哒～");
        } else if (point >= 60 && point < 80) {
            System.out.println("你的信用一般般咯");
        } else {
            System.out.println("你的信用不及格啦:(");
        }
    }
    else{
        System.out.println("好好输入数字喔 1-100 :(");
    }
    }
}

```

  <br>

### 嵌套分支

基本介绍 - 在一个分支结构中又嵌套了另一个完整的分支结构，里面分支的结构称为内层分支，外面的分支结构称为外层分支 规范：不要超过3层 - 破坏可读性

**1.基本语法**

```java

if (){
    if(){
        //if-else
    }else{
        //if-else
    }
}

```

**2.应用案例**

```java

import java.util.Scanner;
/**
 * 演示嵌套分支练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
       Scanner myScanner = new Scanner(System.in);
       System.out.println("请输入你的名字啦");
       String name = myScanner.next();
       System.out.println(name+"，您好呀，接下来请输入您的成绩");
       double score = myScanner.nextDouble();
       if( score > 8.0 ) {
           System.out.println("请输入您的生理性别");
           char gender = myScanner.next().charAt(0);
           if (gender == '女') {
               System.out.println("恭喜您，进入女子组决赛啦！");
           } else {
               System.out.println("恭喜您，进入男子组决赛啦！");
           }
       }
       else {
           System.out.println("抱歉你被淘汰啦");
       }
       }
    }

```

**3.课后练习题**

```java

import java.util.Scanner;
/**
 * 演示嵌套分支练习
 * 出票系统：根据淡旺季的月份和年龄，打印票价
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        Scanner myScanner = new Scanner(System.in);
        System.out.println("请问您想预定1-12月中哪个月份的票呀～");
        int month = myScanner.nextInt();
        if( month == 4 || month == 5 || month == 6 || month == 7 || month == 8
        || month == 9 || month == 10){
            System.out.println("目前正处旺季喔");
            System.out.println("请问您的年龄～为您计算票价中");
            int age = myScanner.nextInt();
            if(age > 18 && age < 60){
                System.out.println("总共支付60元");
            }else if(age < 18){
                System.out.println("总共支付30元");
            }else{
                System.out.println("总共支付20元");
            }
        } else {
            System.out.println("目前正处淡季喔");
            System.out.println("请问您的年龄～为您计算票价中");
            int age = myScanner.nextInt();
            if(age > 18 && age < 60){
                System.out.println("总共支付40元");
            }else{
                System.out.println("总共支付20元");
            }
        }
    }
}

```

<br>

### switch分支结构 

<br>

**1.基本语法**

```java

switch(表达式){
    case 常量1: //当...
    语句块1;
    break; //跳出switch控制结构 不是结束程序
    
    case 常量2;
    语句块2;
    break;
    
    ...
    
    case 常量n;
    语句块n;
    break;
    
    default:
    default语句块;
    break;

    //解读switch
    //1.switch 关键字 表示switch分支
    //2.表达式 对应一个值
    //3.case常量1: 当表达式的值等于 常量1，就执行 语句块1
    //4.break：表示退出switch
    //5.如果和case常量1匹配，就执行语句块1，如果没有匹配，就继续匹配常量2
    //6.如果一个都没有匹配上，执行default
}

```

<br>


**2.switch基本流程图**

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/12/gkINmSiZcPb5XVl.jpg" alt="j205" >
</div>
{{</md>}}
<br>

**3.快速入门案例**

- 请编写一个程序，该程序可以接收一个字符，比如: a, b, c, d, e, f, g

- a表示星期一，b表示星期二

- 根据用户的输入显示相应的信息，要求使用switch语句完成

```java

import java.util.Scanner;
/**
* 演示Switch练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        思路分析
    1. 接收一个字符，创建Scanner对象
    2. 使用switch来完成匹配，并输出对应信息
    代码
        */

        Scanner myScanner = new Scanner(System.in);
        System.out.println("请输入一个字符(a-g)");
        char c1 = myScanner.next().charAt(0);
        //只要是有值返回都可以看成表达式
        switch(c1){
            case 'a':
                System.out.println("今天是星期一啦");
                break;
            case 'b':
                System.out.println("今天是星期二啦");
                break;
            case 'c':
                System.out.println("今天是星期三啦");
                break;
            case 'd':
                System.out.println("今天是星期四啦");
                break;
            case 'e':
                System.out.println("今天是星期五啦");
                break;
            case 'f':
                System.out.println("今天是星期六啦");
                break;
            case 'g':
                System.out.println("今天是星期日啦");
                break;
            default:
                System.out.println("认真输入数字啦！");
                // default后不需要break 因为都会退出
        }
        System.out.println("退出了switch，继续执行程序");
    }
}

```

<br>

**4.switch注意事项和细节讨论**

- 表达式的数据类型，应和case后的常量**类型一致**，或者是可以**自动转成**可以相互比较的类型，比如输入的是字符char，而常量是int 

```java

public class Main {
    //编写一个main方法
    public static void main(String[] args) {
    char c = 20;
    switch (c){
        case 'a':
            System.out.println("ok1");
            break;
        case 20: //就是这里 要注意
            System.out.println("ok2");
            break;
        case 'c':
            System.out.println("ok3");
            break;
    }
    }
} // c【case后的常量类型】会自动转成【表达式类型】作比较
// 不是【表达式】自动转成【case后的类型】
```

- switch(表达式)中表达式的返回值必须是: ( byte, short, int, char, enum[枚举], String )

```java

public class Main {
    //编写一个main方法
    public static void main(String[] args) {
    double c = 1.2; //错误不允许使用这个类型
    switch (c){
        case 1.1:
            System.out.println("ok1");
            break;
        case 1.2:
            System.out.println("ok2");
            break;
    }
    }
}

```

- case 子句中的值必须是常量(1,'a', 'b'+1)或者是常量表达式，而不能是变量 - 例如上边例子 c 是变量variable 20是常量constant

- default字句是可选的，当没有匹配的case时，执行default / 如果没有default字句又没有匹配任何常量，则没有输出

- break语句用来再执行完一个case分支后使程序跳出switch语句块；如果没有写break，程序会执行到switch结尾
  
<br>

**5.switch课堂练习**

- 第一题：使用switch把小写类型的char型转为大写(键盘输入) - 只转换a, b, c, d, e. 其它的输出”other“

```java

import java.util.Scanner;
/**
* 演示Switch练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //创建Scanner对象
        Scanner myScanner = new Scanner(System.in);
        System.out.println("请输入a-e");
        char c1 = myScanner.next().charAt(0);
        switch (c1){
            case'a':
                System.out.println("A");
                break;
            case'b':
                System.out.println("B");
                break;
            case'c':
                System.out.println("C");
                break;
            case'd':
                System.out.println("D");
                break;
            case'e':
                System.out.println("E");
                break;
            default:
                System.out.println("好好输入字母！");
        }
    }
}

```

- 第二题：对学生成绩大于60分的，输出”合格“。低于60分的，输出”不合格“ （注：输入的成绩不能大于100）- 提示 成绩/60 

```java

import java.util.Scanner;
/**
* 演示Switch练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //创建Scanner对象
        /*
        思路分析
        1 - 这道题可以用分支来完成 但是要求switch
        2 - 这里我们需要进行一个转换, 编程思想 ：
            如果成绩在[60,100], int(成绩/60) = 1
            如果成绩在[0,60), int(成绩/60) = 0
        */
        //代码实现
        Scanner myScanner = new Scanner(System.in);
        System.out.println("请输入你的成绩哦～");
        double score = myScanner.nextDouble();
        //使用if-else 保证输入的成绩是有效的 0-100
        if(score >= 0 && score <= 100) {
            switch ((int) (score / 60)) {
                case 0:
                    System.out.println("小伙伴不合格哦");
                    break;
                case 1:
                    System.out.println("恭喜你合格啦");
                    break;
            }
        } else {
            System.out.println("输入的成绩在0-100才有效哦！");
        }
    }
}

```

- 第三题：根据用于指定月份，打印该月份所属的季节 - 3 4 5 春季 6 7 8 夏季 9 10 11 秋季 12 1 2 冬季 课堂练习 提示使用穿透

```java

import java.util.Scanner;
/**
* 演示Switch练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
            思路分析
            1 - 创建一个Scanner对象，接收用户输入
            2 - 使用一个变量类型接收
            3 - 使用switch来匹配，使用穿透完成，比较简洁
        */
        Scanner myScanner = new Scanner(System.in);
        System.out.println("请输入月份哦 注格式：四月");
        String month = myScanner.next();
            switch (month) {
                case "三月":
                case "四月":
                case "五月":
                    System.out.println("目前是春季喔～");
                    break;
                case "六月":
                case "七月":
                case "八月":
                    System.out.println("目前是夏季喔～");
                    break;
                case "九月":
                case "十月":
                case "十一月":
                    System.out.println("目前是秋季喔～");
                    break;
                case "十二月":
                case "一月":
                case "二月":
                    System.out.println("目前是冬季喔～");
                    break;
                default:
                    System.out.println("输入正确的月份格式才有效哦！");
            }
            System.out.println("感谢您的查询");
    }
}

```

<br>

**6.switch和if的的选择**

- 如果判断的具体数值不多，而且符合byte、short、int、char, enum[枚举], String 这六种类型。虽然两个语句都可以使用，建议使用switch语句
- 其他情况：对区间判断，对结果为boolean类型判断，使用if，if的使用范围更广
  <br>

<hr>


## 循环控制 (for while dowhile 多重循环)

<br>

### for循环控制

基本介绍：听其名知其意，就是让你的代码可以循环的执行
<br>

**1.基本语法**

```java

for(循环变量初始化;循环条件;循环变量迭代){
    循环操作(可以多条语句语句);
}
//for 关键字 - 表示循环控制
//for循环四要素：循环变量初始化；循环条件；循环操作；循环变量迭代
//循环操作，这里可以有多条语句，也就是我们要循环执行的代码
//如果 循环操作(语句)只有一条语句，可以省略{} - 但不建议省略

```

<br>

**2.for循环执行流程的分析**

```java

for( int i = 1; i <= 10; i++){ //作为单独语句i++/++i 都是i=i+1的意思
    System.out.println("这里重复内容"); 
}
//在循环条件中某一个适合一定要为false，否则就会死循环
//当循环条件为假 只是退出for循环 而不是退出整个程序

```

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/12/37DP9hdqeitANgr.jpg" alt="j206" >
</div>
{{</md>}}
<br>

**3.注意事项和细节说明**

- 循环条件是返回一个boolean值的表达式

- for(;循环判断条件) 中的初始化和变量迭代可以写到其他地方，但是两边的分号不能省略

```java

/**
* 演示for循环练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        int i = 1;
        for(; i<= 10;){
            System.out.println("这里重复内容");
            i++;
            // 如果你把i=1这个初始变量放在for后面的括号里
            // 它只能作用在这个循环体内，而放在外边，i的作用域变大
            // 它不仅仅能作用在这个循环内，还可以作用在循环外
        }
        System.out.println("i="+i); //11

        //补充
        int j = 1;
        for(;;){ //表示一个无限循环，死循环+break
            System.out.println("ok"+(j++));
        }
    }
}

```

- 循环初始值可以有多条初始化语句，但要求类型一样，并且中间用逗号隔开

```java

int count = 3;
for (int i = 0, j = 0; i < count; i++, j += 2){
    System.out.println("i="+i+"j="+j);
}

```

- 使用内存分析法，老师分析下面代码输出的是什么 
{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/12/Sv94u6FD5G1MWjm.jpg" alt="j207" >
</div>
{{</md>}}
  <br>


**4.for循环的课堂练习**

- 打印1-100之间所有是9的倍数的整数，统计个数 以及 总和 [化繁为简 / 先死后或]

```java

/**
* 演示for循环练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        // 打印1-100之间所有是9的倍数的整数，统计个数 以及 总和 [化繁为简 / 先死后或]
        // 两个编程思想 - 技巧
        //1. 化繁为简：将复杂的需求拆解成简单的需求，逐步完成
        //2. 先死后活：先考虑固定的值，然后转成可以灵活变化的值
        //
        //思路分析
        //化繁为简
        //1.完成 输出1-100的值
        //2.在输出的过程中，进行过滤，只输出9的倍数
        //3.统计个数 定义一个变量 int count = 0；当条件满足时 count++；
        //4.总和 定义一个变量 int sum = 0；当条件满足时累计 sum += i；
        //先死后活
        //1.为了适应更好的需求，把范围的开始的值和结束的值，做成变量，就更加灵活
        //2.为了更进一步9倍数也做成变量int t = 9
        int count = 0; //统计9的倍数个数的变量
        int sum = 0; //总和
        int star = 10;
        int end = 200;
        int t = 5;//倍数
        for(int i = star; i <= end; i++){
            if(i % t == 0) {
                System.out.println("i=" + i);
                count++;
                sum += i;//累积
            }
        }
        System.out.println("count=" + count);
        System.out.println("sum=" + sum);
    }
}

```

- 完成下面的表达式输出

```java

/**
* 演示for循环练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        // 还是用化繁为简 - 先死后活
        //
        //思路分析
        //1.先输出 0-5
        //2.后面的+是 5-i

        //先死后活
        //1. 5替换成变量 n
        int n = 10;
        for(int i = 0; i<=n; i++){
            System.out.println(i + "+" + (n-i) + "=" + n);
        }
    }
}

```

<br>

### while循环控制

<br>

**1.基本语法**

```java

循环变量初始化;
while(循环条件){
    循环体(语句);
    循环变量迭代;
} 
//说明
//while循环也有四要素
//只不过四要素放置的位置，不一样

```

<br>

**2.while循环执行流程分析**

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/12/WEvtSC4NQfiTJFz.jpg" alt="j208" >
</div>
{{</md>}}

<br>

**3.while 循环的案例**

```java

/**
 * 演示while循环练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        // 输出10句 今天见到你很高兴

        int i = 1; //循环变量初始化
        while(i <= 10 ){ //循环条件
            System.out.println("见到你很高兴");//执行语句
            i++;//循环变量迭代
        }
        System.out.println("退出while循环,继续..");//这个时候i=11
    }
}

```

<br>

**4.注意事项和细节说明**

- 循环条件是返回一个布尔值的表达式
- while循环是先判断再执行语句
  <br>

**5.课堂练习题**

- 打印1-100之间所有能被3整除的数 - 使用while

```java

/**
* 演示while循环练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        // 打印1-100之间所有能被3整除的数
        // 化繁为简，先死后活
        int i = 1;
        int endNum = 100;
        while(i <= endNum ) {
            if (i % 3 == 0) {
                System.out.println("i=" + i);

            }
            i++;//变量自增
        }
    }
}

```

- 打印40-200之间所有的偶数 - 使用while

```java

/**
* 演示while循环练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        // 打印40-200之间所有的偶数 - 使用while
        // 化繁为简，先死后活
        int i = 40;
        int endNum = 200;
        while(i <= endNum ) {
            if (i % 2 == 0) {
                System.out.println("i=" + i);

            }
            i++;//变量自增
        }
    }
}

```

<br>

### do.while 循环控制

<br>

**1.基本语法**

```java

循环变量初始化;
do{
    循环体(语句);
    循环变量迭代;
} while(循环条件);

```

<br>

**2.说明**

- do while 是关键字
- 也有循环四要素，只是位置不一样
- 先执行，再判断，也就是说，一定会至少执行一次
- 最后 有一个 分号;
- while和do.while 区别举例：要账
  <br>

**3.do.while循环执行流程分析**

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/12/HjM23Z8YxsSgcLn.jpg" alt="j209" >
</div>
{{</md>}}

<br>

**4.do.while 示例**

```java

/**
 * 演示do.while循环练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        // 输出10句 很高兴认识你
        int i = 1; //循环变量初始化
        do{
            //循环执行语句
            System.out.println("你好很高兴认识你");
            //循环变量迭代
            i++;
        } while(i <= 10);
        System.out.println("退出do-while 继续执行...");
    }
}

```

<br>

**5.注意事项和细节说明**

- 循环条件是返回一个布尔值的表达式
- do.while循环是先执行，再判断，因此它至少执行一次

<br>

**6.课堂练习题**

- 打印1-100 

```java

/**
* 演示do.while循环练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        int i = 1;
        do {
            System.out.println("i=" + i);
            i++;
        } while (i <= 100);
    }
}

```

- 计算1-100的和

```java

/**
* 演示do.while循环练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        int i = 1;
        int num = 0;
        do {
            System.out.println("i=" + i);
            num += i ;
            i++;
        } while (i <= 100);
        System.out.println("num=" + num);
    }
}

```

- 统计1-200之间能被5整除但不能被3整除的个数

```java

/**
* 演示do.while循环练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //统计1---200之间能被5整除但不能被3整除的 个数
        //化繁为简
        //1. 使用do-while输出 1-200
        //2. 过滤能够被5整除但不能被3整除的个数
        //3. 统计满足条件的个数 int count = 0;
        //先死后活
        //1.范围起始值 1-200 可以做成变量
        //2.能被5整除但不能被3整除的 5 3 也可以改成变量
        int end = 200;
        int a = 5;
        int b = 3;
        int i = 1;
        int count = 0;
        do {
            if(i % a == 0 && i % b != 0) {
                System.out.println("i=" + i);
                count++;
            }
            i++;
        } while (i <= end);
        System.out.println("count=" + count);
    }
}

```

- 如果李三不还钱，则老韩将一直使出五连鞭，直到李三说还钱为止

```java

/**
* 演示do.while循环练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //如果李三不还钱，则老韩将一直使出五连鞭，直到李三说还钱为止
        //[System.out.println("老韩问: 还钱吗？y/n")] do...while
        //化繁为简
        //1. 不停的问还钱吗
        //2. 使用char answer 接收回答, 定义一个Scanner对象
        //3. 在do-while的while中判断 如果是 y 就不再循环
        //一定自己动脑筋
        Scanner myScanner = new Scanner(System.in);
        char answer = ' ';
        System.out.println("老韩使出五连鞭！");
        do{
            System.out.println("老韩问：还钱吗？y/n");
            answer = myScanner.next().charAt(0); //用户输入
            System.out.println("他的回答是" + answer);
        }while(answer != 'y');//判断条件很关键
        System.out.println("还钱了");
    }
}

```

<br>

### 多重循环控制 - 难点和重点

<br>

**1.介绍**

- 将一个循环放在另外一个循环体内，就形成了嵌套循环。其中，for，while，do..while 均可以作为外层循环和内层循环【建议一般使用两层，最多不超过3层，否则，代码的可读性很差】

- 实质上，嵌套循环就是把内层循环当成外层循的循环体。当只有内层循环的循环条件为false时，才会完全跳出内层循环，才可以结束外层的当次循环，开始下一轮的循环

- 设外层循环次数为m，内层为n次，则内层循环实际上需要执行 m * n 次

```java

for(int i = 1; i <= 7; i++){//第一层循环 7 
    for(int j = 1; j <= 2; j++){//第二层循环 2
        System.out.println ("ok~~"); //7*2=14
    }
}

```

<br>

**2.多重循环执行步骤分析**

```java

//双层for Multiply
for(int i = 1; i <= 2; i++){
        for(int j = 1; j <= 3; j++){
            System.out.println ("i=" + i + "j=" + j); 
        }
    }

```

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/12/vLJMYhcXP3lfSms.jpg" alt="j210" >
</div>
{{</md>}}
<br>

**3.应用实例**

- 统计3个班成绩情况，每个班有5名同学，求出各个班的平均分和所有班级的平均分[学生的成绩从键盘输入] + 统计三个班及格人数，每个班有5名同学

```java

import java.util.Scanner;
/**
* 演示多重循环控制练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //统计3个班成绩情况，每个班有5名同学
        //求出各个班的平均分和所有班级的平均分[学生的成绩从键盘输入]
        //
        //思路分析
        //化繁为简
        //1. 先计算一个班，5个学生的成绩，使用 for
        //1.1 创建一个Scanner对象 然后接收用户的输入
        //1.2 得到该班级的平均分, 先定义一个 double sum 把该班级5个学生的成绩累计
        //2. 统计3个班级(每个班5个学生) 平均分
        //3. 所有班级平均分
        //3.1 定义一个变量，double totalScore 累积所有学生的成绩
        //3.2 当多重循环结束后，double totalScore / (3 * 5)
        //4.统计三个班的及格人数
        //4.1 定义变量 int passNum = 0; 当有一个学生成绩 >= 60 passNum++
        //4.2 如果 >= 60 passNum++
        //5.可以优化[效率 可读性 结构] - 增加活性
        //创建 Scanner 对象
        Scanner myScanner = new Scanner(System.in);
        double totalScore = 0; //累积所有学生的成绩
        int passNum = 0; //累积 及格的人数
        int classNum = 3; //班级的个数
        int stuNum = 5; //学生个数
        for( int i = 1; i <= classNum ; i++){//i表示班级

            double sum = 0; //一个班级的总分
            for(int j = 1; j <= stuNum; j++){//j表示学生
                System.out.println("请输入第" + i + "个班的第"+ j + "个学生的成绩");
                double score = myScanner.nextDouble();
                //当有一个学生成绩 >= 60 passNum++
                if(score >= 60) {
                    passNumber++;
                }
                sum += score; //累计
                System.out.println("成绩为"+ score);
            }
            //因为sum是5个学生的总成绩
            System.out.println("sum=" + sum + "平均分=" + (sum / stuNum));
            //把 sum 累积到 totalScore
            totalScore += sum;
        }
        System.out.println("三个班总分=" + totalScore + "平均分=" + (totalScore/classNum*stuNum));
        System.out.println("及格人数=" + passNumber );
    }
}

```

- 打印出九九乘法表

```java

**
* 演示多重循环控制练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        for(int i = 1; i <= 9; i++){
            for(int j = 1; j <= 9; j++){
                System.out.println(i + "*" + j + "=" + i*j);
            }
        }
    }
}

```

<br>

**5.经典的打印金字塔**

- 使用for循环完成下面的立体

- 编写一个程序，可以接收一个整数，表示层数(totalLevel)，打印出金字塔 [化繁为简 先死后活]

```java

/**
* 演示金字塔练习
*/
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*

                *
            *   *
            *     *
            *********

            思路分析
            化繁为简
            1 - 先打印一个矩形
            *****
            *****
            *****
            *****
            *****

            2 - 打印半个金字塔
            * //第一层 有一个*
            ** //第二层 有两个*
            *** //第三次 有三个*
            **** //第四层 有四个*
            ***** //第五层 有五个*

            3 - 打印整个金字塔
            * // 1-1    2*层数-1 - 有4=(总层数-1)个空格
        *** // 2-3   2*2-1 - 有3=(总层数-2)个空格
        ***** // 3-5  2*3-1 - 有2=(总层数-3)个空格
        ******* //4-7  2*4-1 - 有1=(总层数-4)个空格
        ********* //5-9 2*5-1 - 有0=(总层数-5)个空格

            4 - 打印 空心金字塔 [最难]
            * // 1-1   当前行的第一个位置是*，最后一个位置也是*
        * * // 2-2  当前行的第一个位置是*，最后一个位置也是*
        *   * // 3-2 当前行的第一个位置是*，最后一个位置也是*
        *     * //4-2 当前行的第一个位置是*，最后一个位置也是*
        ********* //5-9 全部输出

            先死后活
            5 - 层数做成变量 int totalLevel = 5

        */
        int totalLevel = 12;//层数
        for(int i = 1; i <= totalLevel; i++){;// i表示层数
            //在输出*之前，还要输出 对应空格 = 总层数 - 当前层
            for(int k = 1; k <= totalLevel-i; k++){
                System.out.print(" ");
            }

            //控制打印每层的*个数
            for(int j = 1; j <= 2 * i - 1; j++) {
                //当前行的第一个位置是*，最后一个位置也是*，最后一层全部
                if(j == 1 || j == 2 * i - 1 || i == totalLevel){
                    System.out.print("*");
            } else { //其他情况输出空格
                    System.out.print(" ");
                }
            }

            //每打印完一层的*后，就换行 println本身就换行
            System.out.println("");
        }
    }
}

```

<br>

<hr>


## 跳转控制语句-break

<br>

1.随机生成1-100的一个数，直到生成了97这个数，看看一共用了几次（提示使用(int)(Math.random(*100))+1

```java

/**
 * 演示练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        for(int i = 0; i <= 10; i++){
            // 因为random不能取1，所以乘以100再int完之后最大只有99
            System.out.println((int)(Math.random()*100)+1);
        }
    }
}

```

- 循环，但是循环的次数不知 -> break, 当某个条件满足时，终止循环通过该需求可以说明它流程控制数据的必要性，比如break
  <br>

### 基本介绍

1.break语句用于终止某个语句块的执行，一般使用在switch或者循环[for while do-while]中
<br>

### 基本语法

```java

{   ....
    break;
    ....
}

```

- 以while循环为例的示意图 
{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/12/yuI5rE6sXoHAd9Y.jpg" alt="j211" >
</div>
{{</md>}}
  <br>

### 快速入门

```java

/**
 * 演示break练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        for(int i = 0; i < 10; i++){
            if(i==3){
                break;
            }
            System.out.println("i=" + i);
        }
        System.out.println("退出for循环，继续执行..")
    }
}

```

<br>

### 注意事项和细节说明

1.break语句出现在多层嵌套的语句块中时，可以通过标签指明要终止的是哪一层语句块
2.标签的基本使用

```java

label1: {...
label2:     {...
label3:         {   ...
                    break label2;
                    ...
                }
            }
        }

```

- break语句可以指定退出哪层
- label1 是标签，名字由程序员指定
- break 后指定到哪个label就退出到哪里
- 在实际的开发中，尽量不要使用标签
- 如果没有指定break，默认退出最近的循环体
{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/12/rEUXxQWRn6DPVLk.jpg" alt="j212" >
</div>
{{</md>}}
{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/12/iljLJxawmQ65Hh3.jpg" alt="j213" >
</div>
{{</md>}}

### 课堂练习题

1.1-100以内的数字求和，求出 当和 第一次大于20的当前数 【for+break】

```java

/**
 * 演示break练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //思路分析
        //1 - 循环1-100 求和sum
        //2 - 当sum>20时，记录下当前数，然后break
        //3 - 在for循环外部 定义变量 n / 将 i 放在外部
        int sum = 0;//累积和
        
        //注意i的作用范围在for{}
        int n = 0;
        for(int i = 1; i <= 100; i++){
            sum += i;//累积
            if(sum > 20 ){
                System.out.println("和>20时候，当前数i=" + i);
                n= i;
                break;
            }
        }
        System.out.println("当前和=" + sum);
    }
}

```

```java

/**
 * 演示break练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //思路分析
        //1 - 循环1-100 求和sum
        //2 - 当sum>20时，记录下当前数，然后break
        //3 - 在for循环外部 定义变量 n / 将 i 放在外部
        int sum = 0;//累积和
        //注意这个逻辑顺序 - 先初始-判断-执行[求和以及if判断(输出当前i)]-自增
        int i = 1;
        for(; i <= 100;){
            sum += i;//累积
            if(sum > 20 ){
                System.out.println("和>20时候，当前数i=" + i);
                break;
            }
            i++;
        }
        System.out.println("当前和=" + sum);
    }
}

```

2.实现登录验证，有3次机会，如果用户名为“丁真”，密码“666”提示登录成功，否则提示还有几次机会，请使用for+break完成

```java

import java.util.Scanner;
/**
 * 演示break练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        // 实现登录验证，有3次机会，如果用户名为“丁真”，密码“666”提示登录成功，
        // 否则提示还有几次机会，请使用for+break完成
        //
        // 思路分析
        // 1 - 创建Scanner对象，接收用户输入
        // 2 - 定义String name; String passwd; 保存用户名和密码
        // 3.最多循环三次[登录3次]，如果满足条件就提前退出
        // 4，定义一般变量 int chance 记录还有几次登录机会

        Scanner myScanner = new Scanner(System.in);
        String name = "";
        String passwd = "";
        int chance = 3; //登录一次 就减少一次
        for(int i = 1; i <= 3; i++){ //3次登录机会
            System.out.println("请输入名字");
            name = myScanner.next();
            System.out.println("请输入密码");
            passwd = myScanner.next();
            // 比较输入的名字和密码是否正确
            // 补充说明字符串 的比较 使用的 方法 equals
            // 例子 String name = "林黛玉"；
            // System.out.println(name.equals("林黛玉")); T
            // System.out.println("林黛玉".equals(name)); T
            // 用第二种推荐 可以避免空指针
            if("丁真".equals(name) && "666".equals(passwd)){
                System.out.println("恭喜你，登录成功");
                break;
            }

            //登录的机会就减少一次
            chance--;
            System.out.println("你还有" + chance + "次登录机会" );
        }
    }
}

```

<br>

<hr>




## 控制跳转语句-continue 

<br>

### 基本介绍

1.continue语句用于结束本次循环，继续执行下一次循环
2.continue语句出现在多层嵌套的循环语句体中，可以通过变迁指明要跳过的事哪一层循环，这个和前面的标签的使用的规则一样
<br>

### 基本语法

```java

{   ......
    continue;
    ......
}

```

- 示意图 - while使用continue为例
{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/12/LqZduUFizJHfs6t.jpg" alt="j214" >
</div>
{{</md>}}
<br>

### 快速入门案例

```java

/**
 * 演示continue练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //代码
        int i = 1;
        while(i <= 4){
            i++;
            if (i == 2){
                continue;
            }
            System.out.println("i=" + i);//输出 3 4 5
        }
    }
}

```

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/12/6iHWvtImFzCJ8SM.jpg" alt="j215" >
</div>
{{</md>}}
<br>

### continue 细节案例分析和说明

```java

/**
 * 演示continue练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        label1:
        for(int j = 0; j < 4; j++){
            label2:
            for(int i = 0; i < 10; i++){
                if(i == 2){
                    // 看看分别输出什么值 并分析
                    // continue
                    // continue label2
                    continue ;//等价于label2 
                }
                System.out.println("i =" + i);
                //输出4次[0,1,3,4,5,6,7,8,9]
            }
        }
    }
}

```

```java

/**
 * 演示continue练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        label1:
        for(int j = 0; j < 2; j++){
            label2:
            for(int i = 0; i < 10; i++){
                if(i == 2){
                    // 看看分别输出什么值 并分析
                    // continue
                    // continue label2
                    continue label1;//等价于label2
                }
                System.out.println("i =" + i);
                //输出2次[0,1] 
            }
        }
    }
}

```

<br>

<hr>


## 跳转控制语句-return

<br>

### 介绍

return使用在方法，表示跳出所在的方法，在讲解方法的时候，会详细的介绍，这里我们简单的提一下。注意：如果return写在main方法，退出程序...(以下对比 break/continue/return)
<br>

### 案例对比

```java

/**
 * 演示return练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        for (int i=1; i <= 5;i++ ){
            if(i==3){
                System.out.println("测试"+ i);
                break;
            }
            System.out.println("Hello World!");
        }
        System.out.println("go on..");
    }
}
//最终输出 
//Hello World!
//Hello World!
//测试3
//go on..

```

```java

/**
 * 演示return练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        for (int i=1; i <= 5;i++ ){
            if(i==3){
                System.out.println("测试"+ i);
                continue;
            }
            System.out.println("Hello World!");
        }
        System.out.println("go on..");
    }
}
//最终输出 
//Hello World!
//Hello World!
//测试3
//Hello World!
//Hello World!
//go on..

```

```java

/**
 * 演示return练习
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        for (int i=1; i <= 5;i++ ){
            if(i==3){
                System.out.println("测试"+ i);
                return;
                //当return用在方法时，表示跳出方法
                //如果使用在main，表示退出程序
            }
            System.out.println("Hello World!");
        }
        System.out.println("go on..");
    }
}
//最终输出 
//Hello World!
//Hello World!
//测试3

```

<br>

<hr>


## 本章作业

<br>

### 第一题

某人有100,000元，每经过一次路口，需要交费，规则如下：
(1) 当现金 >50000时，每次交5%
(2) 当现金 <= 50000时，每次交1000
计算该人可以经过多少次路口，要求：使用while break方式完成

```java

/**
 * 第一题
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        某人有100,000元，每经过一次路口，需要交费，规则如下：
        (1) 当现金 >50000时，每次交5%
        (2) 当现金 <= 50000时，每次交1000
        计算该人可以经过多少次路口，要求：使用while break方式完成

        思路分析
        1 - 定义 double money 保存 100000
        2 - 根据题的要求，我们分析出来有三种
                money > 50000
                money >= 1000 && money <= 50000
                money < 1000
        3 - 使用多分支 if-elseif-else
        4 - while+break [money < 1000]
            同时使用一个变量count来保存通过路口
         */

        double money = 100000; //还有多少钱
        int count = 0; //累积过的路口
        while(true){ //无限循环
            if(money > 50000){ //过路口
                //money = money - money * 0.05;
                money *= 0.95; //过了这个路口后，还有这么多钱
                count++;
            } else if (money >= 1000 && money <= 50000){
                money -= 1000;
                count++;
            } else { //钱不够
                break;
            }
        }
        System.out.println("100000 " + "可以过 " + count + "个路口");
    }
}

```

<br>

### 第二题

实现判断一个整数，属于哪个范围：大于0；小于0；等于0

```java

/**
 * 第二题
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        实现判断一个整数，属于哪个范围：大于0；小于0；等于0
        思路分析
        1 - 先用Scanner创建用户对象
        2 - 用 if elseif else 判断范围
         */
        Scanner myScanner = new Scanner(System.in);
        System.out.println("请输入一个整数");
        int integer = myScanner.nextInt();
        if(integer > 0){
            System.out.println(integer + "范围大于0");
        } else if (integer < 0){
            System.out.println(integer + "范围小于0");
        } else {
            System.out.println(integer + "范围等于0");
        }
    }
}

```

<br>

### 第三题

判断一个年份是否为闰年

```java

/**
 * 第三题
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        判断一个年份是否为闰年
        思路分析
        1 - 先用Scanner创建用户对象
        2 - 用 if else 判断是否为闰年
         */
        Scanner myScanner = new Scanner(System.in);
        System.out.println("请输入年份");
        int year = myScanner.nextInt();
        if((year % 4 ==0 && year % 100 !=0) || year % 400 == 0 ){
            System.out.println("这一年是闰年");
        } else {
            System.out.println("这一年不是闰年");
        }
    }
}

```

<br>

### 第四题

判断一个整数是否是水仙花数，所谓水仙花数是指一个3位数，其各个位上数字立方和等于其本身
例如：153 = 1*1*1 + 3*3*3 + 5*5*5

```java

**
 * 第四题
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        判断一个整数是否是水仙花数，所谓水仙花数是指一个3位数，
        其各个位上数字立方和等于其本身
        例如：153 = 1*1*1 + 3*3*3 + 5*5*5
        
        思路分析
        1 - 比如int n = 153；
        2 - 先得到n的百位 十位 个位的数字，使用if判断他们的立方和是否相等
        3 - n的百位 = n / 100
            n的十位 = n % 100 / 10
            n的个位 = n % 10
        4 - 判断即可
         */
        int n = 153;
        int n1 = n / 100;
        int n2 = n % 100 / 10;
        int n3 = n % 10;
        if (n1 * n1 * n1 + n2*n2*n2 + n3*n3*n3 == n){
            System.out.println(n + "为水仙花数");
        } else{
            System.out.println(n + "不是水仙花数");
        }
    }

```

<br>

### 第五题

看看下面的代码输出什么

```

class Demo {
    public static void main(string[] args){
        int m = 0, n = 3;
        if(m > 0){

            if(n > 2)
                System.out.println("OK1")
            else 
                System.out.println("OK2")    
        }
    }
}
// 无输出

```

<br>

### 第六题

输出1-100之间的不能被5整除的数，每5个一行

```java

/**
 * 第六题
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        输出1-100之间的不能被5整除的数，每5个一行

        思路分析
        1 - 先用for语句输出1-100个数
        2 - if执行语句 - 不能被5整除
        3 - 设定输出值为每5个一行 我们使用 int count 统计输出的个数
            count%5==0 说明输出了5个 这时我们输出一个换行控制即可
         */
        int count = 0;
        for(int i = 1; i <= 100; i++){
            if (i % 5 != 0){
                count ++;
                System.out.print(i + " ");

                //判断,每满5个，就输出一个换行
                if(count % 5 == 0){
                    System.out.println();
                }
            }
        }
    }
}

```

<br>

### 第七题 

输出小写的a-z以及大写的A-Z

```java

/**
 * 第七题
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        输出小写的a-z以及大写的A-Z
        考察我们对 a-z编码和for循环的综合使用

        思路分析
        1 - 'b'= 'a' + 1   'c'='a' + 2
        2 - 使用for循环
         */
        for(char c1='a'; c1 <= 'z'; c1++){
            System.out.println(c1 + " ");
        }

        for(char c2='A'; c2 <= 'Z'; c2++){
            System.out.println(c2 + " ");
        }
    }
}

```

<br>

### 第八题

求出1-1/2+1/3-1/4...1/100的和

```java

/**
 * 第八题
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        /*
        求出1-1/2+1/3-1/4...1/100的和

        思路分析
        1 - 1-1/2+1/3-1/4...1/100 = (1/1)-(1/2)+(1/3)-(1/4)...1/100
        2 - 从以上的分析我们可以看到
            一共有100数 分子为1 分母从1-100
            分母为偶数时符号为- 奇数时符号为+
        3 - 我们可以使用for+判断即可完成
        4 - 把结果存放到double sum
        5 - 这里有一个隐藏的陷阱，要把 公式分子1写成1.0才能得到精确的消暑
         */

        double sum = 0;
        for (int i = 1; i <= 100; i++){
            //判断是奇数还是偶数，然后做不同的处理
            if( i % 2 != 0){ //分母为奇数
                sum +=  (1.0/i);
            } else { //分母偶数
                sum -=  (1.0/i);
            }
        } System.out.println("sum=" + sum);

    }
}

```

<br>

### 第九题

求1 + (1+2) + (1+2+3) + (1+2+3+4) +...+ (1+2+3+...+100)的结果

```java

/**
 * 第八题
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //求1 + (1+2) + (1+2+3) + (1+2+3+4) +...+ (1+2+3+...+100)的结果
        //100-1 99-2 98-3
        //思路分析
        //1 - 一共有100项
        //2 - 每一项数值在逐渐增加
        //3 - 很像一个双层循环
        //4 - 使用sum进行累积

        //i 可以表示是第几项 同时也是当前项的最后一个数
        int sum = 0;
        for(int i = 1; i <= 100; i++){ //100项
            for (int j = 1; j <= i; j++){
                sum += j;
            }
        }
        System.out.println("sum = " + sum);

    }
}

```

<br>

<hr>

