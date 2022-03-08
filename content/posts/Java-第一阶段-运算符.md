---
title: "Java-第一阶段-运算符"
subtitle: ""
date: 2022-02-27T10:54:15+08:00
draft: false
author: ""
authorLink: ""
description: "各类运算符查典"
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

## 算术运算符

<br>

### 介绍

算术运算符是对数值类型的变量惊醒运算的，在java程序中使用的非常多
<br>

### 算术运算符一览

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/11/LJ4NTtaCie5Pqf2.jpg" alt="j01" >
</div>
{{</md>}}

<br>

### 算术运算符细节

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/11/iUI5GPgpA1zVkYe.jpg" alt="j02" >
</div>
{{</md>}}

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/11/GQxBnaFXvisMHfE.jpg" alt="j03" >
</div>
{{</md>}}
<br>

### 案例习题

```java 

/**
 * 演示算术运算符的使用 01
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        // /的使用
        System.out.println(10 / 4); //从数学来看2.5 java中为2
        System.out.println(10.0/4); //java是2.5 10.0 为double 精度提升
        double d = 10 /4; // java中为2 但是要转给double 2=>2.0
        System.out.println(d); // 是2.0

        //  %取模 取余数
        // 在%的本质 看一个公式 a % b = a - a / b * b (公式重点)
        // -10 % 3 => -10 - (-10) / 3 * 3 = 10 + 9 = -1
        // 10 % -3 => 10 - 10 / (-3) * (-3) = 10 - 9 = 1
        // - 10 % -3 = (-10) - (10) / (-3) * (-3) = -10 + 9 = -1
        System.out.println(10 % 3); //1
        System.out.println(-10 % 3); // -1
        System.out.println(10 % -3); // 1

        // ++ 的使用
        // 作为独立语句使用 前后++ 都等价
        int i = 10;
        i++;//自增 等价于 i = i + 1；=> i = 11
        ++i;//自增 等价于 i = i + 1；=> i = 12
        System.out.println("i = " + 1); // 12
        /*
        作为表达式使用
        前++: ++i先自增后赋值
        后++: i++先赋值后自增
         */
        int j = 8;
        int k = ++j; // 等价 j=j+1 -> k=j
        System.out.println("k=" + k + "j="+ j ); // 9 9
        int m = 8;
        int n = m++; // 等价 m = n -> m = m + 1
        System.out.println("m=" + m + "n=" + n);
    }
}

```

```java 

/**
 * 演示算术运算符的使用 02
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        int i1 = 10;
        int i2 = 20;
        int i = i1++;
        System.out.print("i="+i); //10
        System.out.println("i2="+i2); //20
        i = --i2;
        System.out.print("i=" +i); //19
        System.out.println("i2=" +i2); //19
    }
}

```

```java

/**
 * 演示算术运算符的使用 03
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //1.需求：
        //假如还有59天放假，问：合XX个星期零XX天
        //2.思路分析
        // (1) 使用int 变量 days 保存 天数
        // (2) 一个星期是7天 星期数weeks：days/7
        // (3)输出
        //3.走代码
        int days = 59;
        int weeks = days / 7;
        int leftDays = days % 7;
        System.out.println(days + "天 合" + weeks + "星期零"
                + leftDays + "天");
    }
}

```

```java

/**
 * 演示算术运算符的使用 04
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //1.需求：
        //定义一个变量保存华氏温度，华氏温度转换摄氏温度的公式为：
        //5/9*(华氏温度-100)，求出华氏温度对应的摄氏温度
        //2.思路分析
        // (1) 先定义double/float huaShi
        // (2) 根据给出的公式，进行计算即可
        //     考虑数学公式合java语言的特性
        // (3) 将得到结果保存到变量double sheShi
        //3.走代码
        double huaShi = 234.5f;
        double sheShi = 5.0 / 9 * (huaShi-100); //加.0保留精度
        System.out.println("华氏度" + huaShi + "对应摄氏度=" + sheShi);
    }
}

```

<br>

<hr>


## 关系运算符

<br>

### 介绍

1.也可以叫比较运算符 / 英文 Relational Operator
2.关系运算符的结果通常都是boolean型 - true/false 
3.关系表达式 - 经常用在if结构的条件句中或循环结构的条件中
<br> 

### 关系运算符一览

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/11/tqJlyPHpSMA7nEU.jpg" alt="j04" >
</div>
{{</md>}}
<br>

### 案例演示

```java

/**
 * 演示关系运算符的使用
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        int a = 9;
        int b = 8;
        System.out.println(a>b); // T
        System.out.println(a>=b);// T
        System.out.println(a<=b);// F
        System.out.println(a<b);// F
        System.out.println(a==b);// F
        System.out.println(a!=b);// T
        boolean flag = a > b; // T
        System.out.println("flag="+ flag);
    }
}

```

<br>

### 细节说明

1.关系运算符结果都是boolean型 - true/false
2.关系运算符组成的表达式，称之为关系表达式 a>b
3.比较运算符”==“不能误写成”=“
<br>

<hr>


## 逻辑运算符

<br>

### 介绍

1.用于连接多个条件（多个关系表达式），最终的结果也是一个boolean值
<br>

### 逻辑运算符一览

分两组学习
1.短路与 &&，短路或 ||，取反 !
2.逻辑与 &，逻辑或 |, ^ 逻辑异或
**(理解小窍门 - 与：有假即假；或：有真即真；取反-相反；异或：同假异真)**

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/11/iU6dzpBsvnkwSVl.jpg" alt="j05" >
</div>
{{</md>}}

- a&b：&逻辑与 - 规则：当a和b同时为tru，则结果为true，否则为 false
- a&&b：&&短路与 - 规则：当a和b同时为true，则结果为true，否则为 false 
- a|b：| 叫逻辑或 - 规则：当a和b，一个为true，则结果为true，否则 false
- a||b：|| 叫短路与 - 规则：当有一个为true，则结果为true，否则 false
- !a：取反 - 规则：当a为true，则结果为false，当a为false，结果为 true
- a^b：逻辑异或 - 规则：当a和b不同，则结果为true，否则为 false
  <br>

### &&和&基本规则

1.从运算结果来看没有太大区别
2.过程使用上有一定区别

```java

/**
 * 演示关系运算符的使用
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //&& 和 & 案例演示
        int age = 50;
        if (age > 20 && age < 90 ){
            System.out.println("ok100");
        }
        // &使用
        if (age > 20 && age < 90 ){
            System.out.println("ok200");
        }

        //区别
        int a = 4;
        int b = 9;
        //对于短路与&&而言，如果第一个条件为false，后面则不再判断
        //对于逻辑与&而言，如果第一个条件为false，后面的条件仍然会判断
        if(a < 1 && ++b < 90){
            System.out.println("ok100");
        }
        System.out.println("a=" + a + "b=" + b);// 4 9 - 说明++b并没有执行

    }
}

```

<br>

### || 和 | 基本规则

```java

/**
 * 演示逻辑运算符的使用
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //||短路或 和 |逻辑或 案例演示
        int age = 50;
        if(age > 20 || age < 30){
            System.out.println("ok100");
        }

        //|逻辑或使用
        if(age > 20 | age < 30){
            System.out.println("ok200");
        }

        //区别
        //1.短路|｜或 - 如果第一个条件为true
        //则第二个条件不会判断，最终结果为true，效率高
        //2.逻辑|或 - 不管第一个条件是否为true，第二个都要判断，效率低

        int a = 4;
        int b = 9;
        if (a > 1 || ++b > 4){
            System.out.println("ok300");
        }
        System.out.print("a="+ a + "b=" + b);// 4 9

    }
}

```

<br>

### 取反 ! 基本规则 ( InverseOperator )

```java

/**
 * 演示逻辑运算符的使用
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //操作是取反 T-F F-T 
        System.out.print(60 > 20); // T
        System.out.print(!(60 > 20));// F
    }
}

```

<br>

### 逻辑异或^基本规则

```java

/**
 * 演示逻辑运算符的使用
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //a^b - 逻辑异或，当a/b不同为true，否则为false - 同假异真
        boolean b = (10 > 1)^(3 < 5);
        System.out.println("b=" + b );
    }
}

```

<br>

### 逻辑运算符练习题

```java

/**
 * 演示逻辑运算符的使用
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
       //第一题
        int x = 5;
        int y = 5;
        if(x++==6 & ++y==6){
            System.out.print(x=11);
            // 得不到执行
            // x++是先比较后自增，所以5不等于6
            // 逻辑与 - True - False 得到为 False
        }
        System.out.println("x=" + x + "y=" + y);//6 6

        //第二题
        int a = 5, b = 5;
        if(x++==6 && ++y==6){
            System.out.print(a=11);
            // 得不到执行
            // x++是先比较后自增，所以5不等于6
            // 短路与 - True - False 得到为 False
        }
        System.out.println("a=" + a + "b=" + b);
        // 6 5 - 短路与前面确定false 后面就不执行了

        //第三题
        int c = 5, d = 5;
        if (x++==5 | ++y==5){
            System.out.print(c=11);
            // 输出成功
            // x++x++是先比较后自增，所以5等于5
            // 逻辑或 - True - False 得到 True
        }
        System.out.println("c=" + c + "c=" + c); // 11 6

        //第四道题
        int e = 5, f = 5;
        if (e++==5 || ++f==5){
            System.out.print(e=11);
            // 输出成功
            // x++x++是先比较后自增，所以5等于5
            // 短路或 - True - False 得到 True
        }
        System.out.println("e=" + e + "f=" + f);
        // 11 5 短路或确定前半部分为ture 后面则不执行
    }
}

```

```java

/**
 * 演示逻辑运算符的使用
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
      // 第五题升级
        boolean x=true, y=false;
        short z=46;
        if((z++==46) && (y=true)) z++;
        // z++先比较再自增等于46 - T z=47 - 短路与先看第一个是否为F T的话继续执行
        // y=true是一个赋值语句 - T 
        // 短路与 两个都是 T - 总 T
        // z++ z=48
        if((x=false) || (++z==49)) z++;
        // x=false是一个赋值语句 - F - 短路或先看第一个是否为T F的话继续执行
        // ++z先自增再比较 z=49 等于49 - T
        // 短路或 有一个T则为T 
        // z++ z=50
        System.out.println("z=" + z);//50
    }
}

```

<br>

<hr>


## 赋值运算符 ( AssignOperator )


<br>

### 介绍

- 赋值运算符就是将某个运算后的值，赋给指定变量
  <br>

### 赋值运算符的分类

1.基本赋值运算符 = int a = 10; 
2.复合赋值运算符 

- +=，-=，*=，/=，%=等 / 重点讲解第一个
- a += b; 等价 a = a + b
- a -= b; 等价 a = a - b 
  <br>

### 案例演示

```java

/**
 * 演示赋值运算符的使用
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
      int n1 = 10;
      n1 += 4;// n1 = n1+4
        System.out.println(n1);// 14 
      n1 /= 3; // n1 = n1 / 3  
      System.out.println(n1); // 4
    }
}

```

<br>

### 赋值运算符特点

- 运算顺序从右往左 int num = a + b + c;
- 赋值运算符的左边 只能是变量，右边 可以是变量、表达式、常量值
  - int num = 20; int num2 = 78 * 34 - 10; int num3 = a;
- 符合赋值运算符等价下面的效果
  - 比如: a += 3 等价于a = a + 3；其他类推
- 复合赋值运算符会进行类型转换
  - byte b = 2; b += 3; b++; 
    `// 复合赋值运算符会进行类型转换`
    `byte b = 3;`
    `b += 2; //等价 b = (byte)(b + 2)`
    `b++; // b = (byte)(b+1)`
    <br>

<hr>


## 三元运算符 (TernaryOperator)

<br>

### 基本语法

条件表达式?表达式1:表达式2；
运算规则：

- 如果条件表达式为true，运算后的结果为表达式1；
- 如果条件表达式为false，运算后的结果是表达式2；
- 口诀[一灯大师：一真大师]
  <br>

### 案例演示

```java

/**
 * 演示三元运算符的使用
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
      int a = 10;
      int b = 99;
      //解读
      //1. a > b 为false
      //2. 返回b--，先返回b的值，再b-- 98
      //3. result 返回结果为99
      //4. 如果是--b 返回就是98
      int result = a > b ? a++ : b--;
      System.out.println("result=" + result); //98
      System.out.println("a=" + a); //10
      System.out.println("b=" + b); //98
    }
}

```

<br>

### 三元运算符使用细节

1.表达式1和表达式2要为可以赋给接收变量的类型(或可以自动转换)

```java

/**
 * 演示三元运算符的使用
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //表达式1和表达式2要为可以赋给接收变量的类型
        //可以 自动转换 或者 强转
        int a = 3;
        int b = 8;
        int c = a > b ? a : b;
        // 如果换成 1.1 : 3.4; 则无法编译 因为double -> int 精度损失
        // 可以这样 (int)1.1 : (int) 3.4 ; 强转
        double d = a > b ? a : b + 3; // int - > double 可以 自动转换
    }
}

```

2.三元运算符可以转成if-else语句
`int res = a > b ? a++ : --b;`
`if (a > b) res = a++;` 
`else res = --b;`
<br>

### 课堂练习

```java

/**
 * 演示三元运算符的使用
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        // 要求 - 实现三个数的最大值
        int n1 = 553, n2 = 33, n3 = 123;
        //思路
        //1.先得到n1 和 n2 中最大的数，得到max1
        //2.然后再求出max1 和 n3 中的最大数，保存到max2
        int max1 = n1 > n2 ? n1 : n2;
        int max2 = n3 > max1 ? n3 : max1;
        System.out.println("最大数=" + max2);

        //使用一条语句实现 但是用上面更清晰 推荐使用上面
        //老师提示：后面我们可以使用更好的方法，比如排序
        int max = n3 > (n1 > n2 ? n1 : n2) ? n3 : (n1 > n2 ? n1 : n2);
        System.out.println("最大数=" + max);
    }
}

```

<br>

<hr>


## 运算符的优先级

1.运算符有不同的优先级，所谓优先级就是表达式运算中的运算符顺序，如下表，上一行运算符总优先于下一行
2.只有单目运算符（第二行 - 针对一个值进行运算 ++a）、赋值匀速符是从右向左运算的

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/11/I6Ejxnw5FGysecz.jpg" alt="j06" >
</div>
{{</md>}}

- ()  ,  {} 等
- 单目运算 ++ --
- 算术运算符
- 位移运算符
- 位移运算符
- 逻辑运算符
- 三元运算符
- 赋值运算符
  <br>

<hr>


## 标识符的命名规则和规范

1.标识符概念

- java对各种变量、方法和类等命名时使用的字符序列称为标识符
- 凡是自己可以起名字的地方都叫标识符 int num1 = 90; 

2.标识符的命名规则 - 必须遵守

- 由26个英文字母大小写，0-9，_或$组成
- 数字不可以开头 int 3ab = 1；//错误
- 不可以使用关键字和保留字，但能包含关键字和保留字
- Java中严格区分大小写，长度无限制 int totalNum = 10; int n=90;
- 标识符不能包含空格 

3.标识符练习

- hsp //ok
- hsp12 //ok
- 1hsp // false
- h-s // false
- x h // false
- h$4 //ok
- class // false
- int // false
- double // false
- public // false
- static // false
- goto // false - 保留字 
- stu_name // ok 下划线可以

4.标识符命名规范 - 更加专业

- 包名：多单词组成时所有字母都小谢 aaa.bbb.ccc // 比如 com.hsp.crm
- 类名、接口名：多个单词组成时，所有单词的首字母大写：XxxYyyZzz [大驼峰]// 比如TankShotGame
- 变量名、方法名：多单词组成时，第一个单词首字母小写，第二个单词开始每个单词首字母大写 xxxYyyZzz [小驼峰 简称驼峰法]
- 常量名：所有字母大写 - 多单词时每个单词用下划线连接：XXX_YYY_ZZZ //比如 定义一个所得税率 TAX_RATE
- 后面我们学习到类/包/接口等时，命名规范要这样遵守，更加详细的看文档
  <br>

### 关键字 

1.关键字的定义和特点 - 不用背

- 定义：被Java语言赋予了特殊含义，用做专门用途的字符串（单词）
- 特点：关键字中所有字母都为小写
  
{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/11/MtlJPcNf486Is1i.jpg" alt="j07" >
</div>
{{</md>}}

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/11/MtlJPcNf486Is1i.jpg" alt="j08" >
</div>
{{</md>}}

### 保留字

1.介绍

- java 保留字：现有java版本尚未使用，但以后版本可能会作为关键字使用。用自己命名标识符时要避免使用这些保留字
  - byValue / case / future / generic / inner / operator / outer / rest / var / goto / const
    <br>

<hr>


## 键盘输入语句

<br>

### 介绍 

- 在编程中，需要接收用户输入的数据，就可以使用键盘输入语句来获取 Input.java，需要一个 扫描器(对象)，就是Scanner
  <br>

### 步骤

- 导入该类的所在包 java.util.*
- 创建该类对象（声明变量）
- 调用里面的功能
  <br>

### 案例演示

要求 - 可以从控制台接收用户信息，【姓名，年龄，薪水】

```java

import java.util.Scanner; //表示把java.util下的Scanner类导入

/**
 * 演示接收用户的输入
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //演示接收用户的输入
        //步骤
        // Scanner类 表示 简单文本扫描器 在java.util 包
        //1 - 引入/导入 Scanner类所在的包
        //2 - 创建 Scanner 对象, new 创建一个对象，体会
        //    myScanner 就是 Scanner类的对象
        Scanner myScanner = new Scanner(System.in);
        //3. 接收用户的输入 使用 相关的方法
        System.out.println("请输入名字");

        //当程序执行到 next 方法时，会等待用户输入
        String name = myScanner.next();//接收用户输入 字符串
        System.out.println("请输入年龄");
        int age = myScanner.nextInt(); //接收用户输入 int
        System.out.println("请输入薪水");
        double sal = myScanner.nextDouble(); //接收用户输入 double
        System.out.println("人的信息如下");
        System.out.println("名字=" + name + "年龄=" + age + "薪水=" + sal);
    }
}

```

<br>

<hr>


## 进制

<br>

### 进制介绍

对于整数，有四种表达方式：
1.二进制：0，1 - 满2进1 以0b或0B开头
2.十进制：0-9 - 满10进1
3.八进制：0-7 - 满8进1 以数字0开头
4.十六进制：0-9以及A(10)-F(15),满16进1 以0x或0X开头表示 此处的A-F不区分大小写
<br>

### 举例说明 - Binary Test

- int n1 = 0b1010; //10
- int n2 = 1010; // 1010
- int n3 = 01010; //520
- int n4 = 0x10101; //65793

```java

/**
 * 演示四种进制
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        // 二进制
        int n1 = 0b1010;
        // 10进制
        int n2 = 1010;
        // 八进制
        int n3 = 01010;
        // 十六进制
        int n4 = 0x10101;
        System.out.println("n1=" + n1);
        System.out.println("n1=" + n2);
        System.out.println("n1=" + n3);
        System.out.println("n1=" + n4);
    }
}

```

<br>

### 进制的图示

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/11/DvRYckxaQNF2Vuq.jpg" alt="j09" >
</div>
{{</md>}}

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/11/uzwqpimDGlBsr5N.jpg" alt="j10" >
</div>
{{</md>}}

- 二进制 - 逢二进一
- 八进制 - 满八进一
- 十六进制 - 满十六进一
  <br>

### 进制的转换（基本功）

1.进制转换的介绍 - 其他进制转十进制 / 其他进制转十进制 / 二进制转其他进制 / 其他进制转二进制

- 二进制转十进制
- 八进制转十进制
- 十六进制转十进制
  <br>

- 十进制转二进制
- 十进制转八进制
- 十进制转十六进制
  <br>

- 二进制转八进制
- 二进制转十六进制
  <br>

- 八进制转二进制
- 十六进制转二进制

<br>

2.其他进制转十进制 

- 二进制转十进制
  - 规则 - 从最低位(右边)开始，将每个位上的数提取出来，乘以2的(位数-1)次方，然后求和
  - 案例：将0b1011 转成十进制的数 - 结果为11 // 128 64 32 16 8 4 2 1 
- 八进制转十进制
  - 规则 - 从最低位(右边)开始，将每个位上的数提取出来，乘以8的(位数-1)次方，然后求和
  - 案例 - 请将0234转成十进制的数 - 结果为 156
- 十六进制转十进制
  - 规则 - 从最低位(右边)开始，将每个位上的数提取出来，乘以16的(位数)次方，然后求和
  - 案例 - 请将0x23A转成十进制的数 - 结果为 570
    <br>

3.十进制转其他

- 十进制转二进制
  - 规则：将数不断除以2，直到商为0为止，然后每步得到的余数倒过来，就是对应的二进制
  - 案例：34 - 0b00100010 (一个字节有8位，所以前面会补两个0)
  {{<md>}}
  <div align="center">
  <img src="https://s2.loli.net/2022/02/11/d7s9vZIFbalrJjw.jpg" alt="j11" >
  </div>
  {{</md>}}
- 十进制转八进制
  - 规则：将数不断除以8，直到商为0为止，然后每步得到的余数倒过来，就是对应的二进制
  - 案例：131 - 0203 
  {{<md>}}
  <div align="center">
  <img src="https://s2.loli.net/2022/02/11/4qmg7bwsKiAfHJn.jpg" alt="j12" >
  </div>
  {{</md>}}
- 十进制转十六进制
  - 规则：将数不断除以16，直到商为0为止，然后每步得到的余数倒过来，就是对应的二进制
  - 案例：237 - 0xED
  {{<md>}}
  <div align="center">
  <img src="https://s2.loli.net/2022/02/11/U8YNykZ7X65Kaej.jpg" alt="j13" >
  </div>
  {{</md>}}
    <br>

4.二进制转八进制和十六进制

- 规则：从低位开始，将二进制数每三位一组，转成对应的八进制数即可
- 案例：ob11010101 - 0235 //第一个0代表八进制
  <br>

- 规则：从低位开始，将二进制数每四位一组，转成对应的十六进制数即可 (二进制转十进制转十六进制)
- 案例：ob11010101 - 0xD5 
  <br>

5.八进制和十六进制转二进制

- 规则：将八进制数每1位，转成对应的一个三位的二进制数即可
- 案例：0237 - 010 011 111 - 0b010011111 / 0b10011111
  <br>

- 规则：将十六进制每1位，转成对应的一个四位的二进制数即可
- 案例：0x23B - 0b001000111011
  <br>

<hr>


## 位运算的思考题

1.请看下面的代码，回答a,b,c,d,e结果是多少？
2.请回答在Java中，下面的表达式运算的结果是:(位操作)
<br>

### 二进制在运算中的说明

1.二进制是逢2进1的进位制，0、1是基本算符
2.现代的电子计算机技术全部采用的是二进制，因为它只使用0、1两个数字符号，非常简单方便，易于用电子方式实现。计算机内部处理的信息，都是采用二进制数来表示的。二进制（Binary）数用0和1两个数字及其组合来表示任何数，数字1在不同的位置上代表不同的值，按从右至左的次序，这个值以二倍递增

### 原码、反码、补码 (重点 难点)

网上对原码、反码以及补码的解释过于复杂 - 精简 - 背下来
对于有符号的而言：

- 二进制的最高位是符号位：0表示正数 1表示负数 (口诀: 0->+ 1->-)
- 正数的原码，反码，补码都一样 - 三码合一
- 负数的反码 = 它的原码符号位不变，其他位取反 (0->1 1->0)
- 负数的补码 = 它的反码+1 / 负数的反码=负数的补码-1
- 0的反码，补码是0 
- java没有无符号数，换言之，java中的数都是有符号的
- 计算机在运算的时候，都是**以补码的方式运算**-补码解决正数负数/将两个统一
- 当我们在看运算结果的时候，要看原码 (!!重点)
  <br>

<hr>


## 位运算符 (BitOperator)

1.java中有7个位运算(& | ^ ~ >> << >>>) 分别是按位与&、按位|、按位异或^、按位取反～，他们的运算规则是

- 按位与& - 两位全为1，结果为1，否则为0
- 按位或| - 两位有一个为1，结果为1，否则为0
- 按位异或^ - 两个一个为0，一个为1，结果为1，否则为0
- 按位取反～ - 两个一个为0，一个为1，结果为1，否则为0
- 比如 2&3=0100 ～-2= ～2= 2|3= 2^3=
  <br>

### & | ^ ~ 案例演示

```java

/**
 * 演示位运算
 */
public class Main {
    //编写一个main方法
    public static void main(String[] args) {
        //推导过程
        //1. 先得到2的原码 00000000 00000000 00000000 00000010 一个int是四个字节 一个字节占8个bit
        //   2的补码 00000000 00000000 00000000 00000010
        //2. 3的补码 3的原码 00000000 00000000 00000000 00000011
        //   3的补码 00000000 00000000 00000000 00000011
        //3. 按位与&
        //   00000000 00000000 00000000 00000010
        //   00000000 00000000 00000000 00000011
        //   00000000 00000000 00000000 00000010 & 运算后的补码
        //   运算后的原码 也是 00000000 00000000 00000000 00000010
        //   结果就是 2
        System.out.println(2&3);// 2

        //推导过程
        //1. 先得到-2的原码 10000000 00000000 00000000 00000010
        //2. -2的反码 11111111 11111111 11111111 11111101
        //3. -2的补码 11111111 11111111 11111111 11111110
        //4. 运算后的补码 00000000 00000000 00000000 00000001
        //5. 结果看运算后补码对应的原码 原码就是这个值 00000000 00000000 00000000 00000001 => 1
        System.out.println(~-2);// 1

        //推导过程
        //1.先得到2的原码 00000000 00000000 00000000 00000010
        //2.2的补码-相同 00000000 00000000 00000000 00000010
        //3.运算后的补码 11111111 11111111 11111111 11111101
        //4.结果看运算后的原码 (先反码=补码-1 再反码符号为不变其他取反 - 倒推)
        //  先得到运算后的反码 
        //                  11111111 11111111 11111111 11111100
        //  运算后补码对应的原码(反码符号为不变其他取反) 
        //                  10000000 00000000 00000000 00000011 -> -3
        System.out.println(~2); //-3
    }
}

```

### 习题

<br>

### >> << >>> 案例演示

- 算术右移>>：低位溢出，符号位不变，并用符号为补溢出的高位
- 算术左移<<：符号位不变，低位补0
- 逻辑右移 >>> 也叫无符号右移动 运算规则为低位溢出 高位补0
- 特别说明：没有 <<< 符号 
  `int a=1>>2; // 1=>00000001 => 00000000 本质 1/2/2=0`
  `int c=1<<2; // 1=>00000001 => 00000100 本质 1*2*2=4`
  `int d=4<<3; // 4*2*2=32`
  `int e=15>>2; // 15*2*2=3`
  <br>

<hr>


## 本章作业

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/11/nWQRU2cNosejtga.jpg" alt="j14" >
</div>
{{</md>}}

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/11/WvZxjUctywi5MNh.jpg" alt="j15" >
</div>
{{</md>}}

- 如果要把字符串转成对应的整数要用包装类 integer.parselnt

4.尝试写出将String转成double类型的语句，以及将char类型转成String的语句，举例说明即可，写简单代码
`String str = "18.8";//注意字符串要可以被转成double`
`double d1 = Double.parseDouble(str);`

`char c1 = '林';`
`String str2 = c1 + "";`
<br>
